# Work Summary: Devising optimal pipeline networks

Fall 2019

John Fay and Lincoln Pratson

### Objectives

Building on our initial efforts to construct a set of optimized pipeline networks connecting biogas sources to existing natural gas pipelines in Duplin county, our goal here is to compute the aggregate volume of gas passing through each pipeline segment in the network. This, in turn, would allow us to compute the minimum diameter of each pipeline segment, and from that the cost to construct the overall network.  

We again applied our technique to three pipeline scenarios, each scenario differing on how they connect to the existing network (single connection point vs. multiple) and on the order in which they are added (sorted by least cost to connect vs. random). 

### Methods

##### Graph construction

We computed aggregate flows by converting the pipeline configuration to a directional graph, with edges identified as segments occurring between any bifurcation along the pipeline network. Edges along the upstream periphery of the graph, i.e., those linking biogas sources to the network, were assigned weights equal to the biogas flow rate ($scf/hr$) of the respective source. All other edges, i.e. those just transporting biogas downstream, were assigned a weight of zero. ([code](https://github.com/johnpfay/BioGas_optimization/blob/master/scripts/LCP-pipeline-to-edgelist.ipynb)). 

##### Upstream flow rate accumulation

We then iterated through each edge in this graph, identified all edges from that edge (including the edge itself), and computed the summed weights, which would equal the total upstream biogas flow rate ([code](https://github.com/johnpfay/BioGas_optimization/blob/master/scripts/EdgeList-to-Pipewidths.ipynb)).

##### Conversion to pipe diameter and pipe cost

Once flow rate for each segment was determined, we computed the pipeline diameter required to allow that volume to pass using a feed flow rate function determined by regressing values found in the literature: 
$$
diameter(in.)  = 0.0506 * flow\ rate(scf/h)^{0.3942}
$$
And from diameter we computed cost as: 
$$
Pipeline\ cost($/mi) = 10829 * diameter(in.) ^{0.4854}
$$

---

### Pipeline Results

The figures below show the diameter of pipeline required for each network configuration. The existing natural gas pipeline network is shown in orange. Biogas sources are shown as blue circles with the size proportional to the amount of biogas yield.

![biogas source](WorkSummary_Sept2019.assets\BiogasSource_key.jpg)

Pipelines are shown in green, with thicknesses proportional to their diameter:

![pipe diameter](WorkSummary_Sept2019.assets\PipeDiameter_key.jpg)



#### 1. Single connection point.

<img src=".\WorkSummary_Sept2019.assets\SingleConnect.jpg" alt="SingleConnect" style="zoom:75%;" />

#### 2. Multiple connection point



#### 3. Random order