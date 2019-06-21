---
Title: Biogas Optimization Project
Author: John.Fay@duke.edu
Date: Summer 2019
---

# BioGas Optimization

An ArcPy based workspace to compute an optimized pipeline configuration connecting biogas sources to existing natural gas pipelines in southeast North Carolina. 



### Data requirements

* CSV file of known biogas sources: lat/long coordinate pairs and annual biogas production estimates (mmBTU/year)
* Feature class of existing natural gas pipeline and/or connection points
* Raster cost surface for constructing pipeline



### Package requirements

* Geopandas: for working with spatial features

* Scikit-image: for computing cost distances

  

### Workflow

* For each biogas source location:

  * Compute a cost distance raster away from it: store as Numpy array
  * Add it to a stack of cost distance Numpy arrays

* From the stack of Numpy arrays: 

  * Identify the "break even" areas from each source for a given energy price: 

    * Convert biogas production to $$ 
    * Identify cost distance areas falling within this $$

    