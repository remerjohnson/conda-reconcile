# Setting up an environment for OpenRefine reconciliation with Anaconda

OpenRefine provides a crucial tool in linked data reconciliation (AKA, "from strings to things"). Unfortunately, many of the scripts used to set up local reconciliation services require certain python libraries and/or versions of python itself that can lead to code errors or, worse, dependency hell.  

![dependency hell](https://i0.wp.com/imgs.xkcd.com/comics/cautionary.png)


To avoid this, we will rely on a python environment set up by [Anaconda](https://conda.io/docs/intro.html). Making a virtual environment ensures that we can switch into it whenever we want to reconcile stuff in OpenRefine, and switch back out when we want to do other python stuff (there's lots of other cool python stuff you can do!).  

Once Anaconda is installed, setting up the environment becomes copying and pasting one line on the command line.  

## Pre-requisite installation of Anaconda3

**NOTE:** For this particular repo, we are assuming a Windows user. This is the use case I am faced with, but it would in general work on other systems following those systems' instructions.  

+ Uninstall previous versions of Anaconda on your computer, if they exist.
+ Download the latest version of [Anaconda3 for Windows](https://www.continuum.io/downloads), selecting the Python 3.x version 64-bit installer.  
+ Open the installer, use the default settings, ensuring the boxes about adding conda to your PATH are checked.
+ When finished installing, close the installer, and open "Anaconda Navigator" (you can search Programs for "Anaconda").
+ Click on the "Environments" tab on the left. You should see an environment called `root`. This is where a bunch of popular python libraries have been installed. We will now create a new environment.  

## Set up the new refine conda environment

Conda Navigator has an intuitive GUI for looking at your conda environments, but unfortunately it is not the right tool to set up very specific conda environments like we need. So it's off to the command line! But first:  

+ Download the YAML (`.yml`) file from this repo or clone it however you normally use GitHub.

_For using the command line, Git Shell will work nicely. Or you can use "Anaconda Console" which you got when you installed Anaconda._  

+ Open your shell, and navigate to where you downloaded the YAML file from this repo. Then type:
```
$ conda env create -f openrefine.yml
```  

+ The environment will now be installed, and it should now show up in the Anaconda 'Environments' tab. We're now ready to use the reconciliation scripts.

## Specific Reconcilation Services Breakdown

Now that we have a proper environment set up, we can call the desired service when needed, then let OpenRefine know where to listen in on our local computer to use it.

### FAST

### GeoNames

### Library of Congress (id.loc.gov)

### VIAF (Note: not provided for in this repo)
