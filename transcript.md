# Transcript

## Slide 1 (cover)

Hello, and thank you for joining this short talk about iSEE, a Bioconductor package that provides a graphical user interface for the interactive and collaborative exploration of large-scale transcriptomics data.

My name is Kevin Rue-Albrecht. I am a computational biologist in the group of David Sims at the University of Oxford, and where a large part of my responsibilities is to prepare and deliver training materials as an instructor for the Oxford Biomedical Data Sience training programme.

## Slide 2

iSEE delivers interactive web-applications that can be run locally in RStudio Desktop or accessed on a web-server hosting the application using any major web browser, including Google Chrome, Mozilla Firefox, and Apple Safari.
The graphical user interface includes a number of panels, each with a dedicated functionality, from dimensionality reduction results, to sample or gene metadata, or values from experimental assays.

## Slide 3

iSEE uses the RStudio shiny R package, and won the 1st prize of the world-wide RStudio Shiny contest in 2019 for "Most technically impressive" app among more than 100 submissions.

## Slide 4

iSEE applications feature a wide range of useful functionality.
One of the key features of iSEE is the ability of panels to select data points in some panels and transmit those selections to one or more other panels.

## TODO

- Quatuor of developers (1 slide)
- Introduce Bioconductor
- Introduce SummarizedExperiment / SingleCellExperiment (containers)
- Introduce single-cell analysis in Bioconductor (OSCA)
- iSEE(sce)
- iSEE(..., initial)
- iSEE()
- Runs on RStudio Desktop (locally) or RStudio Server / RStudio Connect (remote server)
- Individual apps can either be tied to one dataset or offer a selection of datasets from which users can choose on the app landing page
- Code tracker
