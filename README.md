# conda-reconcile: An Anaconda-based OpenRefine Reconciliation Environment

## Pre-requisite Anaconda installation

+ **(Windows-only)** [Visual C++ Build Tools](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2017): Scrolls down and select the "Build Tools for Visual Studio 2019" download.  
+ Download [Anaconda3](https://www.anaconda.com/distribution/), selecting the Python 3.x version 64-bit installer, and install it.    
  + **(Windows)** During installation use the default settings, and ensure the boxes that add `conda` to your PATH are checked.

## Setup this `conda` environment

+ Download the YAML (`openrefine.yml`) file from this repo or clone it.
+ `cd` to where you downloaded the YAML file.
+ Create the `conda` environment from the YAML file:  
```
$ conda env create -f openrefine.yml
```  
+ Activate the environment:  
```
$ source activate refine3
```
+ If your shell complains (and/or you are using [Anaconda Prompt](https://conda.io/docs/user-guide/install/windows.html#updating-conda)), instead drop the `source` part:
```
$ activate refine3
```

Depending on your shell, it should say `(refine3)` in your command prompt.  

## Next steps

Make sure you have activated the environment as per above (you must see a `refine3` in your prompt).
+ Download or clone an existing reconciliation service
  + [FAST](https://github.com/remerjohnson/conda-reconcile/wiki/Linked-Data-Reconciliation-Services-Breakdown#fast-reconciliation)  
  + [GeoNames](https://github.com/remerjohnson/conda-reconcile/wiki/Linked-Data-Reconciliation-Services-Breakdown#geonames) (**Note:** requires special setup of API user account)
  + [Library of Congress](https://github.com/remerjohnson/conda-reconcile/wiki/Linked-Data-Reconciliation-Services-Breakdown#library-of-congress-idlocgov)
  + [VIAF](https://github.com/remerjohnson/conda-reconcile/wiki/Linked-Data-Reconciliation-Services-Breakdown#viaf-note-not-provided-for-in-this-repo)
  + [Wikidata](https://github.com/remerjohnson/conda-reconcile/wiki/Linked-Data-Reconciliation-Services-Breakdown#wikidata-note-not-provided-for-in-this-repo) (**Note:** newer versions of OpenRefine have built-in reconciliation to Wikidata)
+ Open your shell
  + `cd` to where you saved the reconciliation service
  + Run it (It runs in the background. You will connect to it via OpenRefine)
    + `$ python script_name.py`
+ Open OpenRefine to begin [reconciliation](http://freeyourmetadata.org/reconciliation/)
  + [Detailed instructions](https://github.com/remerjohnson/conda-reconcile/wiki/Linked-Data-Reconciliation-Services-Breakdown) on running the reconciliation.
