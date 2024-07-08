
Identification pilots for the [World Flora Online](https://www.worldfloraonline.org/)

The World Flora Online (WFO) is a project which aggregates information about plant species. It uses a taxonomic backbone to organise descriptive information (textual descriptions and images). A subset of the project partners are working on identification tools. This "ID task force" group has proposed a number of pilots, this github organisation is a container for these projects.

Currently the pilots are:

1. [text2matrix](https://github.com/WFO-ID-pilots/text2matrix) - using a set of fields from the community (the "Taxonomic Expert Network" reposonsible for managing a subset of the dat in the WFO), this pilot will examine if we can harvest descriptions from the WFO and use a large language model to reformat these into a matrix format, suitable for ingestion into an identification system like xper.
2. [explaindiff](https://github.com/WFO-ID-pilots/explaindiff) - using species identification on images (eg the [PlantNet](https://plantnet.org) system), this pilot aims to help users develop an understanding of plant identification. Specifically, when a computer vision application like PlantNet provides a user with two closely ranked candidate species, we would like to be able to expalin the differences between the two speices in non-tehcnical language. This pilot will use decrsiptive data from the WFO and pass pairs of species descriptions to a large language model in order to get non-technical summaries of the differences between them.
