# Transcript

## Cover slide

Hello, and thank you for joining this short talk about iSEE, a Bioconductor package that provides a graphical user interface for the interactive and collaborative exploration of large-scale transcriptomics data.

My name is Kevin Rue-Albrecht. I am a computational biologist in the group of David Sims at the University of Oxford. Part of my responsibilities is to prepare and deliver training materials as an instructor for the Oxford Biomedical Data Science training programme, while I also develop and maintain software for the analysis of omics data sets, including single-cell omics.

## iSEE

The iSEE package delivers interactive web-applications that can be run locally in RStudio Desktop or accessed on a web-server hosting the application using any major web browser, including Google Chrome, Mozilla Firefox, and macOS Safari.
The graphical user interface includes a range of panels, each with a dedicated functionality, from dimensionality reduction results, to sample or gene metadata, or values from experimental assays.
The user interface is extremely flexible, with the ability to add, remove and rearrange panels.
Additionally, the application allows users to implement new panels types and seamlessly integrate those alongside built-in panel types

## Winners of the 1st Rstudio Shiny Contest

For interactivity, iSEE uses the popular R package `shiny` from RStudio.
In fact, iSEE won the 1st prize of the first RStudio Shiny contest organised in 2019 for "Most technically impressive" app among more than 100 submissions.

## Team effort

iSEE is not solely my work but the collaboration of four talented postdoctoral researchers.
Incidentally, it is a beautiful example of an organic collaboration initiated during an informal discussion at a conference in December 2017, and has led to a great collaboration and friendship as well as several other fruitful outputs together.

## Bioconductor

iSEE is part of the Bioconductor project, a scientific initiative established in 2001 with the mission to promote the statistical analysis and comprehension of current and emerging high-throughput biological assays.
Over the years, the project has accumulated over three thousand software and data packages catering for many different omics technologies, from gene expression microarrays to the wide range of sequencing based technologies.
Single cell omics are no exception, motivating the development of a growing collection of packages providing infrastructure and analytical tools for the analysis and integration of multi-omics single-cell data sets.
One of the great strengths of the Bioconductor project relies on the interoperability between packages accepted in the repository, allowing users and developers to write arbitrarily complex workflows that combine the functionality of multiple packages while operating on common data structures.
In this context, iSEE leverages the information accumulated during those analytical workflows, offering an interactive graphical user interface to conveniently explore and visualise those results.

## SingleCellExperiment

In particular, one of the latest developments in the Bioconductor infrastructure is the SingleCellExperiment class of S4 objects.
This extension of the earlier SummarizedExperiment class is capable of storing all the essential information for most single-cell experiments in a single object.
This makes it a convenient and powerful data structure that has become the de facto currency for Bioconductor packages processing single-cell data.
At its core, the SingleCellExperiment class stores assay data for each feature and cell in matrix format at various stages of the processing workflow.
However, the object also includes components to store metadata for both features and cells, as well as dimensionality reduction results.
Crucially, all of that information is kept synchronised during reordering and subsetting operations on the object.

## Parameter boxes

The stability and convenience of the SingleCellExperiment allows iSEE to automatically discover and parse the information available in any given object.
In turn, that information is used to populate the graphical user interface with interactive control inputs allowing users to access, combine, and visualise individual pieces of information, focusing on what they are trying to achieve rather than how.
User inputs are subdivided into three categories: data, visual, and selection.
For instance, we see here that the first panel on the left, in its data parameters box, has selected the TSNE dimensionality reduction results for display, in a dropdown menu that can be used to instantly switch to any other dimensionality reduction result available in the object.
At the bottom, we also catch a glimpse of the visual parameters box, which can be used to control the colour, shape, and other visual aspects of the panel plot.
On the right, a different type of panel can be used to visualise assayed values for one specific feature in the data set.
To that end, the panel provides a slightly different set of user inputs, some of which are visible in the data parameter box.
For instance, we see that the gene CD3D is selected in the first dropdown menu, and assayed values are taken from the matrix of log-transformed counts, selected in the third dropdown menu.

## Transmitted selections

One of the most exciting features of iSEE is the ability to select data points in some panels and use those selections for highlighting or subsetting in one or more other panels.
In iSEE, selections can be made using the rectangular brush built in the shiny package, or using our bespoke lasso selection using waypoints.
The "Selection parameters" box associated with each panel controls which selection to use in the panel, and how the selection is used by the receiving panel.
For instance, the receiving panel can be restricted to display only the data points selected in the panel where the selection was made, as seen in the middle panel, or the selected data points can simply be highlighted in the receiving panel, as seen on the right. 
Furthermore, although not illustrated here, iSEE supports multiple selections, allowing users to use individual selections or their union in the receiving panels.

## Code tracker

One of the major caveats of many interactive applications is the lack of reproducibility, specifically the lack of transparency about how data are processed behind the scene, and the inability to programmatically reproduce the outputs of an interactive session, or to produce batches of figures inspired from those obtained during the interactive session.
iSEE features a unique code tracker that tracks and displays the exact code run behind the scene to generate each panel output.
The code tracker can be open using the download icon in the top right corner of the application’s navigation bar.
When the application is run locally in RStudio, that code can be run as in the current R session to reproduce exactly the output of every panel in the interface.

## Panel settings

Another common limitation of interactive applications is the inability to restore a session and resume work from a given state.
For this, iSEE dynamically tracks and reports another short script that reflects the current state of every panel in the application.
This script can be used to preconfigure applications that are launched in a certain state.
A state includes the relative size of panels, as well as the value of every user input in the interface, including the variables shown for the x and y axis, the choice of colouring for data points, but also selections and transmission links between panels.
For instance, several research groups have used that functionality to complement their published work with publicly accessible iSEE applications that directly showcase essential aspects of the data set to their visitors.

## Preconfigured appliations

Practically, the initial state of an iSEE application is nothing more than a list of panels, each with their own configuration of user inputs.
As I mentioned, the initial state of an application can be exported from the state of an earlier session, but they can also easily be written and configured by hand.
All that is needed is then to pass that configuration to the `iSEE()` function, which builds and configure the application before it is run and served to the user.

## Guided tours

All of this information can be overwhelming to new users.
For this, iSEE includes the possibility to design guided tours, that users can launch from the using the question mark icon in the top right corner of the application’s navigation bar.
Each step in a guided tour attaches a message to an element of the interface.
Together, the steps of a guided tour can guide users through key aspects of a data set, or simply train them to use the user interface efficiently.

## Developing new panels

As I mentioned at the very start, iSEE allows users to develop new panels that seamlessly integrate alongside built in panels in the user interface.
Panels are implemented as a hierarchy of S4 classes, some of which provide core functionality shared by all the panel types that are derived from it.
In other words, new panels can be rapidly developed by re-using and extending functionality available in other panel types.
Our separate package `iSEEu` provides a number of additional panel types demonstrating this functionality.
In particular, I want to a moment here to stress that the built-in panels in iSEE are restricted to display information already present in the object.
In other words, built-in panels do not compute new information.
However, some panels in the `iSEEu` package demonstrate how users can develop panels that do compute new information.
For instance the `DynamicReducedDimensionPlot` is designed to receive a selection of data points from another panel, and dynamically compute and display a new dimensionality reduction result for that selection.

## TODO

- Landing page
- iSEE(sce)
- iSEE()
- Runs on RStudio Desktop (locally) or RStudio Server / RStudio Connect (remote server)
- Individual apps can either be tied to one dataset or offer a selection of datasets from which users can choose on the app landing page
