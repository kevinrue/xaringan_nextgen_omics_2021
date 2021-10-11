# Transcript

## Cover slide

Hello, and thank you for joining this short talk about iSEE, a Bioconductor package that provides a graphical user interface for the interactive and collaborative exploration of large-scale transcriptomics data.

My name is Kevin Rue-Albrecht. I am a computational biologist in the group of David Sims at the University of Oxford, and where a large part of my responsibilities is to prepare and deliver training materials as an instructor for the Oxford Biomedical Data Sience training programme.

## iSEE

iSEE delivers interactive web-applications that can be run locally in RStudio Desktop or accessed on a web-server hosting the application using any major web browser, including Google Chrome, Mozilla Firefox, and Apple Safari.
The graphical user interface includes a number of panels, each with a dedicated functionality, from dimensionality reduction results, to sample or gene metadata, or values from experimental assays.

## Winners of the 1st Rstudio Shiny Contest

iSEE uses the RStudio shiny R package, and won the 1st prize of the world-wide RStudio Shiny contest in 2019 for "Most technically impressive" app among more than 100 submissions.

## Team effort

This is of course not solely my work but the shared sweat and tears of four talented postdoctoral researchers.
Incidentally, it is a beautiful example of organic collaboration initiated during an informal discussion at a conference in December 2017, and has led to several other fruitful outputs to date.

## Bioconductor

<!--
It might be more natural to introduce Bioconductor here.
-->

## Slide 4

iSEE applications feature a wide range of useful functionality.
However, one of the key features that motivated the development of iSEE is the ability of panels to select data points in some panels and transmit those selections to one or more other panels.
Selections can be made using the rectangular brush builtin the shiny package, or using our bespoke lasso selection using waypoints.
The "Selection parameters" box associated with each panel controls how each selection is used by the receiving panel.
The panel can be restricted to display only the data points selected in the panel where the selection was made, as seen in the middle panel, or the selected data points can simply be highlighted in the receiving panel, as seen on the right. 

## TODO

- Introduce Bioconductor
- Introduce SummarizedExperiment / SingleCellExperiment (containers)
- Introduce single-cell analysis in Bioconductor (OSCA)
- iSEE(sce)
- iSEE(..., initial)
- iSEE()
- Runs on RStudio Desktop (locally) or RStudio Server / RStudio Connect (remote server)
- Individual apps can either be tied to one dataset or offer a selection of datasets from which users can choose on the app landing page
- Code tracker
