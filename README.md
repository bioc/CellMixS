## CellMixS
  
A toolbox to explore group-/batch-specific bias and data integration in single-cell RNA-seq (scRNA-seq) datasets.  

### Motivation

Data integration and batch effect correction belong to the major challenges in scRNA-seq.  
A variety of tools and methods have been developed to address them in different ways.
To apply those it is key to understand their effect as well as the underlying technical variation in the data.
Thus new tools and metrics are needed, that help to explore, quantify and compare batch effects in the context of data integration and batch effect removal.  
Similar to biological triggers and signals, batch effects can affect cells in different ways. 
To explore them with cell-specific metrics can help us to better understand, correct and interpret them.

### Description  

Here we provide a toolbox to explore and compare group effects in single-cell RNA-seq data. 
It has two major applications:  
  
* Detection of batch effects and biases in single-cell RNA-seq data.    
* Evaluation and comparison of data integration (e.g. after batch effect correction).  
  
For this purpose it introduces two new metrics:  

* **Cellspecific Mixing Score (cms)**: A test for batch effects within k-nearest neighbouring cells.     
* **Local Density Differences (ldfDiff)**: A score describing the change in relative local cell densities by data integration or projection. 

Besides this, several exploratory plotting functions enable evaluation of key integration and mixing features.  

### Installation

To run CellMixS, open R and install from GitHub using the following commands: 

```
if (!requireNamespace("BiocManager"))
    install.packages("BiocManager")
BiocManager::install("CellMixS")
```

### Getting started
The main metrics `cms` and `ldfDiff` use a `SingleCellExperiment` object as input. 
You need to specify the batch variable as defined in the `colData`, the number of k-nearest neighbours to include `k` and optional the reduced dimensions to use `red_dim`.

```
sce_cms <- cms(sce, k = 70, group = "batch")
```

As `ldfDiff` compares the dataset structure before and after integration you need to specify unaligned and aligned `SingleCellExperiment` objects:

```
sce_ldf <- ldfDiff(sce_pre_list, sce_combined, group = "batch", k = 70)
```
Please have a look into the vignette for details.

### Examples

You can explore batch effects by visualizing metrics and batches aside.

![](/inst/extdata/cms_screenshot1.png)

The histogram of `cms` score can be read like a p.value histogram and is flat for random batch mixing (**batch100**). 
If a batch related bias is present a high number of low `cms` scores can be seen (**batch0**).

![](/inst/extdata/visHist_cms.png)

