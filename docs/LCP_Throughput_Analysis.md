## LCP Throughput Analysis

#### Objective: 

Take the LCP feature class generated from the LC-Pipeline-Construction.ipynb file and compute the total amount of gas going through each segment of pipeline. 

#### Challenges: 

1. The result of the LC-Pipeline-Construction script is not topologically clean; segments into which later pipelines are connected do not necessarily have a node at the junction. This needs to be repaired before an edge list and/or network dataset can be created. 

2. ArcGIS Pro does not have the capability to create network datasets from scratch. ArcGIS Desktop must be used either to create the network dataset or to create a template from which ArcGIS Pro can create one. 
3. The biogas source attributes need to be linked to the network and a downstream accumulative trace be created. 
4. An alternate approach of using the traceback raster created in the Scikit-Image MCP procedure can be explored. 

#### Workflow:

1. Generate a LCP feature class using the LC-Pipeline-Construction script: `./scratch/LCP_Network.shp`.

2. In ArcGIS Desktop:

   1. Create a new file geodatabase: `LCP_analysis.gdb`

   2. Within this geodatabase, construct a new feature datasets: `LCP_datasets` (same spatial reference as LCP feature class).

   3. Import the `LCP_network.shp` into this feature dataset as `SingleConnectPoint`.

   4. Construction a Network Dataset via the New Network Dataset wizard

      > Name: LCP_datasets_ND
      > Type: Geodatabase-Based Network Dataset
      > Version: 10.1
      >
      > Sources: 
      >   Edge Sources: 
      >     SingleConnectPoint
      >
      > Connectivity: 
      >   Group 1: 
      >     Edge Connectivity: 
      >       SingleConnectPoint (End Point)
      >
      > Elevation Model: None
      >
      > Attributes: 
      >   Length: 
      >     Usage Type: Cost
      >     Data Type: Double
      >     Units Type: Meters
      >     Use by Default: True
      >     Source Attribute Evaluators: 
      >       SingleConnectPoint (From-To): Field
      >           Language: VBScript
      >           Expression: [Shape]
      >       SingleConnectPoint (To-From): Field
      >           Language: VBScript
      >           Expression: [Shape]
      >     Default Attribute Evaluators: 
      >       Default Edges: Constant = 0
      >       Default Junctions: Constant = 0
      >
      > Directions: 
      >   Directions Configured: No
      >     -To configure directions at least one edge source must have a mapped street field name
      >
      > Optimizations: 
      >   Service Area Index: Yes

