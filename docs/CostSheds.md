# Biogas "cost-shed" analysis

### Objective

Our goal here was to identify, in one quick sweep, all areas in a Duplin Co. that are cost effective to construct pipes to connect various biogas sources at a given price point. We aimed to do this by developing a surface where each pixel represents the minimum cost to deliver biogas to that location - from any biogas source. With this surface, we would then be able to reveal all areas that are cost effective to connect at a given price point simply by selecting pixels with values at or below that price point.

### Methods

The first step in creating this surface involved generating a set of cost distance surfaces, one originating from each biogas source and depicting the minimum cost to pipe methane to any location from that source. The values in these cost distance surfaces are not just a factor of the distance away from a given biogas source, but also the the volume of gas produced (sites producing more biogas can transport it more cheaply on a per-unit basis) and the media across which the biogas must be transported. Thus to produce these cost-distance surfaces, we first computed the base transport cost ($\$/mi-MMBtu @ 15 years$) for each biogas source (based on its production capacity), and then multiplied this base cost by a cost-multiplier surface (the MIT cost surface) which increases the base cost from 1 to 3 times based on the land cover in which it passes. That then serves as the input for a minimum cost path algorithm that accumulates cost as distance is traveled outward from the biogas source. We then added the cost of biogas production at the given source to the cost distance values so that each pixel's value in the resulting layer would be the total cost (production and delivery) to get one unit of biogas to that location from that site. 

Once we generated the set of cost distance layers for each biogas source in Duplin County, we then computed the minimum cost distance value across all layers at each pixel location: this minimum cost layer then represents the least cost value for any pixel to get a unit of biogas to that location. The figure below shows the resulting surface. Heights are the minimum cost-distance and the one black dot represents the biogas source with the lowest production cost. ![](C:\Workspace\Gits\BioGas_optimization\docs\CostSheds.assets\Surface3d.png)

What we found, however, was that the cost to construct pipelines anywhere was quite small relative to the cost of production such that it would nearly always be cheapest to pipe biogas from the one site shown above because its production - and pipeline - costs were still much lower than production costs alone. 

The figure below illustrates this. It shows the same surface as above, but now shows the production costs along the Z-axis for all other biogas sources. It clearly shows that the production costs are all quite higher than the minimum cost surface driven by the cheapest biogas source.

![](C:\Workspace\Gits\BioGas_optimization\docs\CostSheds.assets\SurfaceAndPoints.png)