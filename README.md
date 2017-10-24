# conda-reconcile: An Anaconda-based OpenRefine Reconciliation Environment

## Pre-requisite Anaconda installation

+ **(Windows-only)** [Visual C++ Build Tools](http://landinghub.visualstudio.com/visual-cpp-build-tools): select the "Download Visual C++ Build Tools 2015" option.  
+ Download [Anaconda3](https://www.continuum.io/downloads), selecting the Python 3.x version 64-bit installer, and install it.    
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
+ If your shell complains, instead drop the `source` part:
```
$ activate refine3
```

Depending on your shell, it should say `(refine3)` in your command prompt.  

## Next steps

Download and run (via `python script_name.py`) the [reconciliation services](https://github.com/remerjohnson/conda-reconcile/wiki/Linked-Data-Reconciliation-Services-Breakdown) for your desired vocabulary:
+ [FAST](https://github.com/remerjohnson/conda-reconcile/wiki/Linked-Data-Reconciliation-Services-Breakdown#fast-reconciliation)  
+ [GeoNames](https://github.com/remerjohnson/conda-reconcile/wiki/Linked-Data-Reconciliation-Services-Breakdown#geonames) (**Note:** requires special setup of API user account)
+ [Library of Congress](https://github.com/remerjohnson/conda-reconcile/wiki/Linked-Data-Reconciliation-Services-Breakdown#library-of-congress-idlocgov)
+ [VIAF](https://github.com/remerjohnson/conda-reconcile/wiki/Linked-Data-Reconciliation-Services-Breakdown#viaf-note-not-provided-for-in-this-repo)
+ [Wikidata](https://github.com/remerjohnson/conda-reconcile/wiki/Linked-Data-Reconciliation-Services-Breakdown#wikidata-note-not-provided-for-in-this-repo) (**Note:** newer versions of OpenRefine have built-in reconciliation to Wikidata)
