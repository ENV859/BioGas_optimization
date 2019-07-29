# Least cost pipeline procedure

## Step 1. Create stacks of biogas cost & cost distance layers

First, for each biogas source, we create two products used in the optimization procedure: 

1. <u>A cost layer</u> whereby each pixel's value represents the cost to pipe gas from that source through that pixel.  Cost is a factor of the volume produced at the source and the land type through which it is passing. 
2. <u>A cost-distance layer</u> whereby each pixel's value represents the accumulated cost to construct pipeline from the biogas source to that pixel's location. 

These are produced by iterating through a table of biogas sources, sorted in ascending order of transport cost ($\$/mi{-}MMBtu$). A cost surface is generated (by multiplying the source's transport cost to each value in the MIT cost-factor surface), and then a cost distance surface is generated from that. 

The cost and cost-distance layers produced are added to a cost and a cost-distance layer stack, respectively. These stacks are saved as both multi-band geoTIFFs (viewable in ArcGIS) and NumPy export arrays (easily imported into later Python scripts). 



## Step 2. Identify the optimal pipeline connection point

The next step involves finding the point along the existing NG pipeline that would be least costly to connect to any biogas source and then to construct the least cost path linking that source to the pipeline at this location. 

* First, we convert the Hart Energy pipeline data to a raster matching the cell size and dimensions as the cost and cost-distance layers constructed above. This allows us to isolate pixels corresponding to pipeline locations. 
* Then, for only pipeline pixels, we determine the minimum cost value among all cost-distance layers, and then determine at which pipeline pixel this minimum occurs: this would be our connection point. 
* We also determine to which layer, of the stack of all biogas cost-distance layers, 
* 