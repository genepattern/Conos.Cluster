# Perform joint clustering of multiple datasets with Conos

**Description**: Conos.Cluster implements the joint embedding and clustering setps for the Clustering On Networks of Samples pipeline for integrating multiple single cell datasets into a common lower-dimensional embedding. Requires the output of the Conos.Preprocess module.

**Contact**: [genepattern.org/help](https://genepattern.org/help)

**Author(s)**:  Kharchenko Lab, Department of Biomedical Informatics, Harvard Medical School. <br> Wrapped as a module by Anthony S. Castanza, Edwin Juárez, and Barbara A. Hill Mesirov Lab, UCSD School of Medicine.

**Summary**: This is step 2 of 3 in the Conos pipeline. The Conos.Preprocess module requires that datasets first be processed by the Conos.Preprocess module into an RDS object. The initial joint KNN graph constructed by the Conos.Preprocess module will be clustered using either or both of the leiden community clustering, or walktrap clustering methods, and then this clustered joint-graph will be embedded into a joint lower-dimensional space using the UMAP method.

**Source Publication**: Barkas N., Petukhov V., Nikolaeva D., Lozinsky Y., Demharter S., Khodosevich K., & Kharchenko P.V. 
Joint analysis of heterogeneous single-cell RNA-seq dataset collections. 
Nature Methods, (2019). doi:10.1038/s41592-019-0466-z <br>
See: [https://github.com/kharchenkolab/conos](https://github.com/kharchenkolab/conos) for full citation information

**Pipeline**: The complete pipeline utilizing the Conos workflow is available as a notebook at [Conos Integration for scRNA-seq](https://notebook.genepattern.org/hub/preview?id=442)

**Parameters:**

| Name | Description |
|:----------------|:----------------------------------|
| conos_object | Conos object created by Conos.Preprocess. |
| runleiden | True/False. Whether or not to run Leiden community clustering. |
| leiden_resolution | Resolution for Leiden Community Clustering (default:1). Generally best performance is achieved with a resolution between 1 and 2 |
| runwalktrap | True/False. Whether or not to perform runwalktrap community clustering. |
| walktrap_steps | Number of steps to be taken for the walktrap algorithm (default:10) |
| umap_distance | UMAP Minimum Distance (default: 0.05) |
| umap_spread | UMAP Spread (default: 5.0) |

**Output**:

The primary outputs of the Conos.Cluster module are a number of PNG files that contain representations of the joint graph constructed by Conos. A non-exhaustive list of important outputs is given here.

<ul>
<li> The Per-sample_Global_[Clustering]_Clusters_Individual_UMAP.png file displays the input datasets separately but with harmonized clusters.</li>
<li> The Per-sample_Global_[Clustering]_Clusters_Common_UMAP.png file displays the same clusters, but with each sample projected into the common UMAP embedding generated from the joint graph.</li>
<li>The [Clustering]_Cluster_Composition.png file displays the per cluster cohort mixing and is useful for evaluating how well those cohorts mixed.</li>
<li>Additional plots are also produced for both individual and shared clustering and embeddings.</li>
</ul>

The output of the Conos.Cluster module also contains an RDS object object that contains the main conos object under $con, if leiden clustering was run under $runleiden, if walktrap clustering was run under $runwalktrap, and the data source under $data_source (seurat or matrix).

```
# Save an object to a file
saveRDS(list(con = con, runleiden = runleiden, runwalktrap = runwalktrap, data_source = data_source), 
 "conos_cluster_output.rds")
print("saved conos_cluster_output.rds")```

**Module Language**: R 

## Technical note:
This module uses the Conos Docker container vpetukhov/conos:version-1.4.4 wrapped in the container genepattern/conos:2.1 <br>
[The source code for this module is maintained in the Conos Dockerfile repository.](https://github.com/genepattern/docker-conos)
