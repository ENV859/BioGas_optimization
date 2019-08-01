# Work Summary: Devising optimal pipeline networks

Summer 2019<br>John Fay and Lincoln Pratson

### Objectives

We have constructed a set of optimized pipeline networks to connect the biogas sources in Duplin county to existing natural gas pipeline networks. The pipeline networks differ on how they connect to the existing network (single connection point vs. multiple) and on the order in which they are added (sorted by least cost to connect vs. random). Our objectives in developing these different networks are (1) to build and refine the algorithm used to optimize a least cost pipeline network, and (2) explore the cost sensitivity to different pipeline network optimization approaches. 

### Pipeline Results

Below is a figure of a pipeline network connecting Duplin Co biogas sources (black dots) via a single connection point along the existing pipeline (light blue). The connection point is identified as the point along the existing natural gas pipeline network with the lowest pipeline connection cost to any biogas source. The process adds a pipeline from the least cost source to that connection point. From there, additional sources are added to the network in order of lowest cost distance to the network established in the previous iteration. 

![SingleConnect](C:\Workspace\Gits\BioGas_optimization\docs\WorkSummary.assets\SingleConnect.png)

Here, the pipeline segments are color coded by cost to connect with yellow being the least cost, to green, blues, and finally violets which represent the highest cost and last connected biogas sources. The network can therefore be thresholded to reveal the biogas sources that can be connected given a specific cost constraint. The shades of gray in the back depicts the pipeline cost surface with lighter shades depicting land features that increase pipeline construction costs. 



The next figure shows the same sources connected via multiple connection points to existing natural gas pipelines. The symbology is  as above. 

![MultipleConnect](C:\Workspace\Gits\BioGas_optimization\docs\WorkSummary.assets\MultipleConnect.png)



And finally, the following figure shows pipelines connected in a random order, but connected in a least costly fashion given pipelines that had been connected in previous iterations.

![RandomAdd](C:\Workspace\Gits\BioGas_optimization\docs\WorkSummary.assets\RandomAdd.png)

### Cost evaluations

Plots of the pipeline construction cost accumulated as more biogas sources are added indicate that the two optimized construction processes (single connection vs multiple connection) are virtually identical, while the randomly added sites incurred higher costs relative to the other two. Interestingly, the total cost to add all sites is equal among the three approaches. 

![](C:\Workspace\Gits\BioGas_optimization\docs\WorkSummary.assets\PipelineCostPlot.png)

Below is a plot showing the the cost of adding biogas sources against revenue generated. Here revenue is computes by multiplying the total yield of a given site ($scf/h$) by a hypothetical cost, here \$0.02 per $sfc/h$. The inflection point at about 290 sites added indicates where the cost to connect a site exceeds the revenue gained. 

![](C:\Workspace\Gits\BioGas_optimization\docs\WorkSummary.assets\CostVsRevenue_2cents.png)