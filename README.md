# Setting up an environment for OpenRefine reconciliation with Anaconda

OpenRefine provides a crucial tool in linked data reconciliation (AKA, "from strings to [things](https://www.wikidata.org/wiki/Q61694)"). Reconciliation by its nature, tends to be first automated by a machine, then manually reviewed by a human since semantics are involved, which makes OpenRefine's combination of a GUI and scripting support an ideal tool. Unfortunately, this functionality does not always come "out of the box", and many of the scripts used to then set up "local" reconciliation services require certain python libraries and/or versions of python _itself_ that can lead to code errors or, worse, dependency hell.  

![dependency hell](https://i0.wp.com/imgs.xkcd.com/comics/cautionary.png)


To avoid this, we will rely on a python environment I have made with [Anaconda](https://conda.io/docs/intro.html). Anaconda makes python virtual environments so that you can tailor one to a specific task or program (thus avoiding the previously mentioned dependency hell). Making a virtual environment ensures that we can switch into it whenever we want to reconcile stuff in OpenRefine, and switch back out when we want to do other python stuff (there's [lots of other cool python and other programming stuff](http://programminghistorian.org/lessons/) you can do!).  

If you're curious what types of libraries are included, they mainly have to do with [SPARQL](https://en.wikipedia.org/wiki/SPARQL) to query linked data sources, as well as common libraries that are designed to interact with APIs, and finally libraries that attempt ["fuzzy matching"](https://en.wikipedia.org/wiki/Record_linkage#Probabilistic_record_linkage).  

Once Anaconda is installed, setting up the environment becomes copying and pasting one line on the command line.  

**NOTE:** For this particular repo, we are assuming a Windows user. This is the use case I am faced with, but it would in general work on other systems following those systems' instructions (and in fact, will require fewer steps). This environment has been successfully built on Windows7 and Windows10 machines.  

## Pre-requisite installation of Microsoft C++ Build Tools

One first pre-requisite: Microsoft needs some special "build tools" to work with certain python libraries. Visit the [Visual C++ Build Tools page](http://landinghub.visualstudio.com/visual-cpp-build-tools) and select the "Download Visual C++ Build Tools 2015" option. Let the installer run, and go get some coffee, because it might take a while.

## Pre-requisite installation of Anaconda3

+ Uninstall previous versions of Anaconda on your computer, if they exist.
+ Download the latest version of [Anaconda3 for Windows](https://www.continuum.io/downloads), selecting the Python 3.x version 64-bit installer.  
+ Open the installer, use the default settings, ensuring the boxes about adding `conda` to your PATH are checked.
+ When finished installing, close the installer, and open "Anaconda Navigator" (you can search Programs for "Anaconda"). This is Anaconda's GUI.  
+ Click on the "Environments" tab on the left. You should see an environment called `root`. This is where a bunch of popular python libraries have been installed. We will now create a new environment.  

## Set up the new refine conda environment

Conda Navigator has an intuitive GUI for looking at your `conda` environments, but unfortunately it is not the right tool to set up very specific `conda` environments like we need. So it's off to the command line! But first:  

+ Download the YAML (`.yml`) file from this repo or clone it... however you normally grab repositories from GitHub.

_NOTE: For using the command line in the rest of these instructions, Git Shell (that gets installed with GitHub Desktop) or Git Bash will work nicely. Or you can use "Anaconda Console" which you got when you installed Anaconda._  

+ Open your shell, and navigate (via `cd`) to where you downloaded the YAML file from this repo. Alternatively, if you have the Git Bash program installed, you can right-click in the directory with the YAML file and select the "Git Bash here" option from the context menu.  
+ Type:  
```
$ conda env create -f openrefine.yml
```  

+ The environment will now be installed, and it should now show up back in the Anaconda Navigator 'Environments' tab as `refine3`.

+ Now go back to your shell. We want to switch into our new environment. In `conda`, we do that by typing:

```
$ source activate refine3
```

If your shell complains, instead drop the `source` part:
```
activate refine3
```

Depending on your shell, it will probably now say `(refine3)` somewhere on your command prompt. We're now ready to grab and use the reconciliation scripts.

## Specific Reconciliation Services Breakdown

Now that we have a proper environment set up, we can call the desired service when needed, then let OpenRefine know where to listen in on our local computer to use it.

### FAST reconciliation

I have a forked version of the FAST reconciliation script called [fast-reconcile](https://github.com/remerjohnson/fast-reconcile).  

+ Clone the repo.
+ In your shell while in the refine3 environment, `cd` in, and type:

```
$ python reconcile.py
```
+ The shell should report that the service is running and note which port, something like `Running on http://0.0.0.0:5000/`.
+ Open OpenRefine, select the column you would like to reconcile, click on the arrow at the top, choose `Reconcile` > `Start Reconciling...`
+ Click on the Add Standard Service button in the bottom left corner.
+ Now enter the URL that the local service is running on - it should be `http://localhost:5000/reconcile`
+ You should now be greeted by a list of possible reconciliation types for the service. Choose your desired options and then click `Start Reconciling`.
+ Whenever you are finished and wish to close the service down, hit `Ctrl` + `C` to stop it.  

Note that this is the first-time set up. OpenRefine will save that service, but you must still beforehand activate the `conda` environment and run the script.  

### GeoNames

We will use Christina Harlow's service, [geonames-reconcile](https://github.com/cmh2166/geonames-reconcile).  

The instructions are the same as above for FAST, except one crucial bit: it relies on a GeoNames API user name. So first:

+ Go to the [login page](http://www.geonames.org/login) and register. After your account is activated, [enable it for free web services](http://www.geonames.org/manageaccount).
+ Once you have your GeoNames username, create an environment variable on your computer with your Geonames username as so:
  + Open your shell
  + Type in `$ export GEONAMES_USERNAME="username"` (replacing username with your username)
+ Proceed as above in the FAST reconciliation

### Library of Congress (id.loc.gov)

We will use Christina Harlow's service [lc-reconcile](https://github.com/cmh2166/lc-reconcile).

The instructions are the same as above for FAST, except the local URL to use when selecting `Standard Service` in OpenRefine is `http://localhost:5000/`.

Optionally, you could ignore this local version and run the hosted verion by putting instead the URL `http://lc-reconcile.cmh2166.webfactional.com/`.  

### VIAF (Note: not provided for in this repo)

Although there used to be a python-based VIAF reconciliation service, it has since moved to a much bigger Java-based framework called [conciliator](https://github.com/codeforkjeff/conciliator).  

Conciliator has grown to provide reconciliation for way more than just VIAF, including ORCID, and any Solr data source.

Since Java set up is beyond the scope of this repo, read the manual, and [use the hosted version of conciliator](http://refine.codefork.com/) if you don't wish to install it locally.  

### Wikidata (Note: not provided for in this repo)

Wikidata reconciliation is quickly becoming a highly-desired ability, and there is a [Wikidata Hosted Reconciliation Service](https://tools.wmflabs.org/openrefine-wikidata/). In order to use it, simply choose to reconcile a column in OpenRefine, then add the API endpoint as a "Standard Service": https://tools.wmflabs.org/openrefine-wikidata/en/api.   

**Update:** In the latest releases of OpenRefine, 2.7+, you can now reconcile to Wikidata right out of the box. Neat!  

## Further Resources

+ [Conda cheat sheet](https://conda.io/docs/using/cheatsheet.html)

## Next Steps

Make a Vagrant box to automate this further.
