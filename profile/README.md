
## Identification pilots for the [World Flora Online](https://www.worldfloraonline.org/)

The World Flora Online (WFO) is a project which aggregates information about plant species. It uses a taxonomic backbone to organise descriptive information (textual descriptions and images). Management of the taxonomic backbone and mobilisation of descriptive data is devolved to a community of Taxonomic Expert networks (TENs). A subset of the project partners (the "ID task force") are working on identification tools. This group has proposed a number of pilots, and this github organisation is a container for these projects.

## Pilot projects
Currently the pilots are:

1. [text2matrix](https://github.com/WFO-ID-pilots/text2matrix) - using a set of fields from the community (the "Taxonomic Expert Network" reposonsible for managing a subset of the data in the WFO), this pilot will examine if we can harvest descriptions from the WFO and use a large language model to reformat these into a matrix format, suitable for ingestion into an identification system like [xper](https://app.xper3.fr/).
1. [explaindiff](https://github.com/WFO-ID-pilots/explaindiffs) - using species identification on images (eg the [PlantNet](https://plantnet.org) system), this pilot aims to help users develop an understanding of plant identification. Specifically, when a computer vision application like PlantNet provides a user with two closely ranked candidate species, we would like to be able to explain the differences between the two species in non-technical language. This pilot will use descriptive data from the WFO and pass pairs of species descriptions to a large language model in order to get non-technical summaries of the differences between them.

## WFO ID task force

The ID task force meets monthly (?) and currently has the following membership:
- Marc Sosef (chair) - research scientist (Flora of Central Africa, Flora of Gabon, African grasses) at Meise Botanic Garden, Belgium. [Institutional profile](https://www.plantentuinmeise.be/nl/pQp2eSN/marc-sosef), ORCID: [0000-0002-6997-5813](https://orcid.org/0000-0002-6997-5813)
- Eve Lucas - senior research leader in accelerated taxonomy at RBG Kew. [Institutional profile](https://www.kew.org/science/our-science/people/eve-j-lucas), ORCID: [0000-0002-7603-435X](https://orcid.org/0000-0002-7603-435X)
- Visotheary Ung - MNHN, Paris. [Institutional profile](https://isyeb.mnhn.fr/en/directory/visotheary-ung-4696), ORCID: [0000-0002-4049-0820](https://orcid.org/0000-0002-4049-0820)
- Nicky Nicolson - senior research leader in digital collections at RBG Kew. [Institutional profile](https://www.kew.org/science/our-science/people/nicky-nicolson), ORCID: [0000-0003-3700-4884](https://orcid.org/0000-0003-3700-4884)
- Young Jun Lee - 3rd-year MBiol Biology student at University of Oxford, summer science intern [Institutional profile](https://www.salgo.ox.ac.uk/people/young-jun-lee), ORCID:[0000-0002-4989-9956](https://orcid.org/0000-0002-4989-9956)

## Other contacts

- Alan Elliot - WFO community manager, RBG Edinburgh [institutional profile](https://www.rbge.org.uk/about-us/who-we-are/staff/major-floras/dr-alan-elliott-bioinformatician/), ORCID: [0000-0002-8677-5688](https://orcid.org/0000-0002-8677-5688)
- Pierre Bonnet - PlantNet. Institutional profile, ORCID: [0000-0002-2828-4389](https://orcid.org/0000-0002-2828-4389)

## Contributing

The github organisation has a [discussion board](https://github.com/orgs/WFO-ID-pilots/discussions) feature - here you can start threaded discussions on the combination of text and image inputs when conducting and analysing plant identifications. Contributions of relevant research papers, software tools etc are welcomed. Each of the pilot projects will also accept contributions as github issues - examine the dedicated project pages for details.
