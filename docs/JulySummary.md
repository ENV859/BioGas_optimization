# Summary of tasks completed

### Scraped biogas source data

### Dairy farm analyses

* Computed distance from geocoded addresses of dairy farms to the nearest known connection points.
* Constructed and delivered various visualizations of the above analysis.

### Organized workspace for analysis of optimized pipeline

* Created GitHub site, Python development environment, and ArcGIS Pro project for analysis
* Consolidated and organized necessary input data
  * MIT Cost Surface
  * DuplinCountySwineFarmEconomics.xlsx
  * Hart Energy Pipeline dataset (*not in workspace, see section below)

### Processed and prepared the Hart Energy pipeline dataset

* Downloaded and stored the raw data files from Hart Energy
  * Located in a directory on ns-leviathan only accessible by LP and JF
  * Backed up on a NSOE research drive
* Uncompressed data files and developed an ArcGIS Pro workspace for viewing the data
  * Project is also located on ns-leviathan
  * Data are accessible via mapped drive -- to LP and JF only
* Developed techniques for maintaining the data one the license has expired
  * Tool for rasterizing state-wide datasets at set resolutions (NC processed only).
  * Tool for reducing gas pipelines to vertices and storing in JSON format along with attributes.
  * Tool for reassembling the pipeline dataset from above JSON format file of vertices.
    * Currently seeking approval that we can retain this format after the license expires...

### Developed algorithms for 