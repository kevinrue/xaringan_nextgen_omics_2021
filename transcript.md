# Transcript

## Cover slide

Hello, and thank you for joining this short talk about iSEE, a Bioconductor package that provides a graphical user interface for the interactive and collaborative exploration of large-scale transcriptomics data.

My name is Kevin Rue-Albrecht. I am a computational biologist in the group of David Sims at the University of Oxford, where a large part of my responsibilities is to prepare and deliver training materials as an instructor for the Oxford Biomedical Data Sience training programme.
I also develop and maintaing software for the analysis of omics data sets, including single-cell omics.

## iSEE

iSEE delivers interactive web-applications that can be run locally in RStudio Desktop or accessed on a web-server hosting the application using any major web browser, including Google Chrome, Mozilla Firefox, and macOS Safari.
The graphical user interface includes a range of panels, each with a dedicated functionality, from dimensionality reduction results, to sample or gene metadata, or values from experimental assays.

## Winners of the 1st Rstudio Shiny Contest

iSEE uses the R package `shiny` from RStudio, and won the 1st prize of the first RStudio Shiny contest organised in 2019 for "Most technically impressive" app among more than 100 submissions.

## Team effort

iSEE is not solely my work but the shared sweat and tears of four talented postdoctoral researchers.
Incidentally, it is a beautiful example of an organic collaboration initiated during an informal discussion at a conference in December 2017, and has led to a great collaboration and friendship as well as several other fruitful outputs together.

## Bioconductor

As I mentioned, iSEE is part of the Bioconductor project, a scientific initiative established in 2001 with the mission to promote the statistical analysis and comprehension of current and emerging high-throughput biological assays.
Over the years, the project has accumulated over three thousand R packages catering for many different omics technologies, from gene expression microarrays to the wide range of sequencing based technologies.
Single cell omics are no exception, motivating the development of a growing collection of packages providing infrastructure and analytical tools for the analysis of transcriptomics and integrative multi-omics single-cell data sets.
One of the great strengths of the Bioconductor project relies on the interoperability between packages accepted in the repository, allowing users and developers to write arbitrarily complex workflows that combine the functionality multiple packages while operating on common data structures.
In this context, iSEE leverages the information accumulated during those analytical workflows, offering an interactive graphical user interface to conveniently explore and visualise those results.

## SingleCellExperiment

In particular, one of the latest developments in the Bioconductor infrastructure is the SingleCellExperiment S4 class of objects. This extension of the earlier SummarizedExperiment class is capable of storing all the essential information for most single-cell experiments in a single object. This makes it a convenient and powerful data structure that has become the currency for Bioconductor packages processing single-cell data. At its core, the SingleCellExperiment class stores the raw and transformed assay data for each feature and cell in matrix format. Additional experimental metadata for both features and cells can be stored in DataFrames, while the matrices of dimensionality reduction results are stored in a separate component of the same object. All of that information is kept synchronised during reordering and subsetting operations.

## Parameter boxes

The stability and convenience of the SingleCellExperiment allows iSEE to automatically parse the information available in the object, and populate the graphical user interface with visual inputs that users can interact with to access and visualise individual pieces of information, focusing on what they are trying to achieve rather than how.
User inputs are subdivided into three categories: data, visual, and selection.
For instance, we see here that the first panel on the left, in its data parameters box, has selected the TSNE dimensionality reduction results for display, in a dropdown menu that can be used to instantly switch to any other dimensionality reduction results available in the object. We also catch a glimpse of the visual parameters box, which can be used to control the color, shape, and other visual aspects of the panel plot.
On the right, a different type of panel can be used to visualise assayed values for one specific feature in the data set. To that end, the panel provides a slightly different set of user inputs, some of which are visible in the data parameter box.

## Transmitted selections

One of the key features that motivated the development of iSEE is the ability to select data points in some panels and use those selections for highlighting or subsetting in one or more other panels.
In iSEE, selections can be made using the rectangular brush built in the shiny package, or using our bespoke lasso selection using waypoints.
The "Selection parameters" box associated with each panel controls how each selection is used by the receiving panel.
The panel can be restricted to display only the data points selected in the panel where the selection was made, as seen in the middle panel, or the selected data points can simply be highlighted in the receiving panel, as seen on the right. 


of panels to select 


## Slide 4

iSEE applications feature a wide range of useful functionality.
However, one of the key features that motivated the development of iSEE is the ability of panels to select data points in some panels and transmit those selections to one or more other panels.

## TODO

- Introduce SummarizedExperiment / SingleCellExperiment (containers)
- Introduce single-cell analysis in Bioconductor (OSCA)
- iSEE(sce)
- iSEE(..., initial)
- iSEE()
- Runs on RStudio Desktop (locally) or RStudio Server / RStudio Connect (remote server)
- Individual apps can either be tied to one dataset or offer a selection of datasets from which users can choose on the app landing page
- Code tracker
