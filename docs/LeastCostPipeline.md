# Least cost pipeline procedure

## Step 1. Create stacks of biogas cost & cost distance layers

First, for each biogas source, we create two products used in the optimization procedure: 

1. <u>A cost layer</u> whereby each pixel's value represents the cost to pipe gas from that source through that pixel.  Cost is a factor of the volume produced at the source and the land type through which it is passing. 
2. <u>A cost-distance layer</u> whereby each pixel's value represents the accumulated cost to construct pipeline from the biogas source to that pixel's location. 

These are produced by iterating through a table of biogas sources, sorted in ascending order of transport cost ($\$/mi{-}MMBtu$). A cost surface is generated (by multiplying the source's transport cost to each value in the MIT cost-factor surface), and then a cost distance surface is generated from that. 

The cost and cost-distance layers produced are added to a cost and a cost-distance layer stack, respectively. These stacks are saved as both multi-band geoTIFFs (viewable in ArcGIS) and NumPy export arrays (easily imported into later Python scripts). 



## Step 2. Identify the optimal pipeline connection point

This notebook imports the cost distance stack generated by `Create-Cost-Stack.ipynb` and a pipeline raster to compute a least cost "feeder" pipeline configuration. The workflow for this process is:
1. Import the stack of cost distance layers (one for each biogas source): $arr\_stack$.
1. Import the pipeline raster, setting non-pipeline cells to no_data: $arr\_pipeline$.
1. Determine which pixel among the pipeline pixels has the least cost among all farm cost distances rasters. This will serve as the location of the connection point to the existing pipeline: $C_0$.
1. Determine which farm is the source of this minimum point, done by finding which layer (in the stack of cost distance rasters) has the minimum value at that location. This represents the least cost biogas source: $F_0$.
1. Compute the least cost path connecting that farm ($F_0$) to the connection point ($C_0$): $LCP_0$.
1. Update the connection point layer ($C_0$) to include the least cost path ($LCP_0$): $Pipes_0$.
1. Remove the layer associated with $F_0$ from the stack of cost distance rasters ($arr\_CDsk$) and repeat steps 4-7:
    * Locate the minimum value among all remaining cost distance rasters to cells in the Pipes layer ($C_i$)...
    * Identify the source farm associated with this minimum ($F_i$)...
    * Compute the least cost path from from $F_i$ to $C_i$...
    * Update the connection point layer ($Pipes_{i+1}$)...
