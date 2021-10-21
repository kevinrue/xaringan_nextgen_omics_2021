# Transcript

## Cover slide

Hello, and thank you for joining this short talk about iSEE, a Bioconductor package that provides a graphical user interface for the interactive and collaborative exploration of large-scale transcriptomics data.

My name is Kevin Rue-Albrecht.
I am a computational biologist in the group of David Sims at the University of Oxford, where part of my responsibilities are to prepare and deliver training materials as an instructor for the Oxford Biomedical Data Science training programme.
I also develop and maintain software for the analysis of omics data sets, including single-cell omics.

## iSEE

The iSEE package delivers interactive web-applications that can be run locally in RStudio Desktop or accessed on a web-server hosting the application using any major web browser, including Google Chrome, Mozilla Firefox, and macOS Safari.
The graphical user interface includes a range of panels, each with dedicated functionality, from displaying dimensionality reduction results, to sample and gene metadata, and values from experimental assays.
The user interface is extremely flexible, with the ability to add, remove and rearrange panels.
Additionally, the application allows users to design new panel types and seamlessly integrate those alongside built-in panel types in the main user interface.

## Winners of the 1st Rstudio Shiny Contest

For interactivity, iSEE uses the popular R package `shiny` from RStudio.
In fact, iSEE was awarded the 1st prize of the first RStudio Shiny contest organised in 2019 for "Most technically impressive" app among more than 100 submissions.

## Team effort

iSEE is the collaboration of four talented postdoctoral researchers, as well contributions and constructive feedback from the broader community of Bioconductor users and developers.
Incidentally, it is a beautiful example of an organic collaboration initiated during an informal discussion at an in-person conference in December 2017, and has led to an ongoing collaboration and friendship as well as several other fruitful outputs together.

## Bioconductor

iSEE is part of the Bioconductor project, a scientific initiative established in 2001, with the mission to promote the statistical analysis and comprehension of current and emerging high-throughput biological assays.
Over the years, the project has accumulated over three thousand software and data packages catering for many different omics technologies, from gene expression microarrays to the wide range of sequencing based technologies.
Single cell omics are no exception, motivating the development of a growing collection of packages providing infrastructure and software for the analysis and integration of multi-omics single-cell data sets.
One of the great strengths of the Bioconductor project relies on the interoperability between packages accepted in the repository, allowing users and developers to write arbitrarily complex workflows that combine the functionality of multiple packages while operating on common data structures with minimal learning curve.
In this context, iSEE leverages the information accumulated during those analytical workflows, offering an interactive graphical user interface to conveniently explore and visualise those results.

## SingleCellExperiment

In particular, one of the latest developments in the Bioconductor infrastructure is the SingleCellExperiment class of S4 objects.
This extension of the earlier SummarizedExperiment class is capable of storing all the essential information for most single-cell experiments in a single object.
This makes it a convenient and powerful data structure that has become the _de facto_ currency for Bioconductor packages processing single-cell data.
At its core, the SingleCellExperiment class stores matrices holding assay data for each feature and cell in the data set at various stages of the processing workflow.
However, the object also includes data components to store metadata for both features and cells, as well as dimensionality reduction results.
Crucially, all of that information is kept synchronised during reordering and subsetting operations on the object, minimising the cognitive load on both users and developers while processing data.

## SingleCellExperiment & iSEE

The stability and convenience of the SingleCellExperiment class allows iSEE to automatically discover and parse the information available in any given data set.
In turn, that information is used to populate the graphical user interface with interactive control inputs giving users the ability to access, combine, and visualise individual pieces of information.
As a result, users are empowered to intuitively focus on _what_ they are trying to achieve, rather than the often convoluted data processing taking place behind the scene to achieve that result.

## Parameter boxes

User inputs are subdivided into three categories: data parameters, visual parameters, and selection parameters.
For instance, we see here that the first panel on the left, in its "data parameters" box, has selected the TSNE dimensionality reduction results for display, in a dropdown menu that can be used to instantly switch to any other dimensionality reduction result available in the object.
At the bottom, we also catch a glimpse of the "visual parameters" box, which can be used to control the colour, shape, and other visual aspects of the panel's plot.
On the right, a different type of panel can be used to visualise assayed values for one specific feature in the data set.
To that end, the panel parameter boxes provides slightly different sets of control inputs, some of which are visible in the data parameter box.
For instance, we see that the gene CD3D is selected in the first dropdown menu, and assayed values are taken from the matrix of log-transformed counts, selected in the third dropdown menu.

## Transmitted selections

One of the most exciting features of iSEE is the ability to select data points in some panels and use those selections for highlighting or subsetting in one or more other panels.
In iSEE, selections can be made using the rectangular brush built in the `shiny` package, or using our bespoke lasso selection using waypoints.
The "Selection parameters" box associated with each panel controls which selection to use in the panel, and how the selection is used by the receiving panel.
For instance, the receiving panel can be restricted to display only the data points selected in the panel where the selection was made, as seen in the middle panel, or the selected data points can simply be highlighted by a color in the receiving panel, as seen on the right. 
Furthermore, although not illustrated here, iSEE supports multiple selections in each panel, allowing users to use individual selections or their union in the receiving panels.

## Code tracker

One of the major caveats of many interactive applications is the lack of reproducibility, specifically the lack of transparency about how data are processed behind the scene, and the inability to programmatically reproduce the outputs of an interactive session, rapidly and easily.
iSEE features a unique code tracker that displays the exact code needed to reproduce each panel output.
The code tracker can be open using the download icon in the top right corner of the application’s navigation bar.
When the application is run locally in RStudio, that code can be run _as is_ in the current R session to reproduce exactly the output of every panel in the interface.
Of course, users can also choose to save the script as a file for future use, or to programmatically generate batches of figures inspired from those obtained interactively in the user interface.

## Panel settings

Another frequent limitation of interactive applications is the inability to save the state of an interactive session, to later resume work from that point.
For this, iSEE dynamically tracks and reports another short script that describes the current state of every panel in the application.
This script can be used to preconfigure applications that can then be launched in a certain state.
A session state includes the relative size of panels, as well as the value of every user input in the interface, including the variables shown for the x and y axes, the choice of colouring covariates, but also the position of selection brushes and the transmission links between panels.
For instance, several research groups have already used that functionality to complement their published work with publicly accessible iSEE applications that directly showcase essential aspects of their data sets to their visitors.

## Preconfigured appliations

Practically, the initial state of an iSEE application is nothing more than a list of panels, each with their own configuration of user inputs.
As I mentioned, the initial state of an application can be exported from the state of an earlier session, but they can also easily be written and configured by hand, as show in the top left corner.
All that is needed is then to pass that configuration to the `iSEE()` function, which builds and configure the application before it is run and served to the user, as shown in the bottom left corner.

## Guided tours

All of this information can be overwhelming to new users.
For this, iSEE includes the possibility to design guided tours, that users can launch from the application’s navigation bar using the question mark icon in the top right corner.
Each step in a guided tour attaches a message to an element of the interface.
Together, the steps of a guided tour can take users through key aspects of a data set, or simply train them to use the user interface efficiently.

## Developing new panels

As I mentioned at the very start, iSEE allows users to develop new panels that seamlessly integrate alongside built in panels in the user interface.
Panels are implemented as a hierarchy of S4 classes, some of which provide core functionality shared by all the panel types that are derived from it.
In other words, new panels can be rapidly developed by re-using and extending functionality available in other panel types.
Our separate package `iSEEu` provides a number of additional panel types demonstrating this functionality.

In particular, I want to take a moment here to stress that the built-in panels in iSEE are restricted to display information _already present_ in the object.
In other words, built-in panels _do not_ compute new information.
However, some panels in the `iSEEu` package demonstrate how users can develop panels that do compute new information.
For instance the `DynamicReducedDimensionPlot` panel type is designed to receive a selection of data points from another panel, and dynamically compute and display a new dimensionality reduction result for that selection.
This is all thanks to `shiny` applications running in an R session giving them access to functionality implemented in all the packages installed in the user's R library.

## Custom landing pages

iSEE was originally designed to serve one data set per application.
However, we have found that for publicly available applications, it can be convenient to centralise multiple data sets in a single application letting users choose a data set at run time.
For this, users can design a custom landing page, where visitors should be presented with at least a choice of data sets, and a button to load the chosen data set in the standard iSEE user interface.
In particular, custom landing pages can be a great way to welcome visitors on a branded web page, while leveraging the functionality of iSEE applications for interactive exploration.

## More

As we are approaching the end of this presentation, I will stress that iSEE is far from restricted to single-cell transcriptomics data sets.
Despite its name, the SingleCellExperiment class is suitable for storing any rectangular data set, from bulk experiments such as RNA-seq or ChIP-seq, to microarray, flow cytometry, and more.
Feel free to come to us with your own use cases, and challenge us to see how your own data types may come to life in iSEE applications!

I will also mention that I could not possibly introduce or demonstrate all the use cases and features of iSEE applications in this presentation.
In the past, we have given up to 3-hour long hands-on workshops and still not entirely covered everything iSEE can do.
One example is the use of cloud-based voice recognition software, giving users voice control of iSEE applications, such as adding or removing panels from the user interface, or coloring data points, matching the voice input to the nearest covariate name in the data set.

Finally, we have also written an online freely available book that imparts knowledge and advice for users wishing to develop their own custom panel types to extend iSEE applications.

## References

With this, I would like to acknowledge the collective work of the Bioconductor community and my collaborators on this project.
The mere idea of `iSEE` could not have been possible without the extensive collection of Bioconductor packages that provide infrastructure and software for the representation and processing of omics data sets.
I am particularly thankful for the positive feedback that we have received during the development of `iSEE` over the last few years.
This has been a great source of motivation and moral support to continue maintaining `iSEE`, as well as delivering conferences presentations and workshops.

## Contact

Finally, I will conclude with contact information for myself and the iSEE project, should you wish to continue the discussion beyond this Next Gen Omics meeting.
You can reach me on Github, Twitter, and LinkedIn.
The iSEE project has a dedicated channel on the Bioconductor Slack workspace, that you are very welcome to join.
This presentation is available in HTML format on my GitHub account, where you will be able to follow the various links throughout my slides.
And lastly, the iSEE project also has a dedicated account on GitHub, where you can find training materials, such as workshops and conference presentations.

With that I would like to thank you all for your attention, and I am happy to take any question during the upcoming Q&A session.
