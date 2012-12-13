Graphiti Project - NYC Graffiti Data Network Edition (part 3 of 3)
============================

Network diagram in Gephi matching graffiti artists to their social graph of associated artistic movements (Graffiit excluded). Data assemble from DB pedia and Freebase exports; completed and cleaned with hours of love.

The original data set can be accessed via the NYC socrata open data portal.

Files in the repo represent the javascript, css/markup for a CartoDB wrapper using Leaflet, Stamen and Colorbrewer to presenting the final mapping visualization from NYC data.

Further explanation can be found in the step-by-step below.

View the project as rendered on this git page: [http://auremoser.github.com/graphitiNet](http://auremoser.github.com/graphitiNet)

Description
===========
Inspired by Graphiti projects 1 and 2 (see graphitiTime and graphitiMap), I wanted to a create network map that would supplement and accessorize New York graffiti data gathered from the NYC open data socrata portal. Increasingly throughout the project I became interested in the place of graffiti art vis-à-vis more formal fine art forms. I wanted to tease out artist relationships to movements, not unlike [Paolo Negrini’s knowledge base of artists] (http://paolonegrini.wordpress.com/2012/11/19/network-map-of-knowledge-and-art/), but instead of tracking influence relationships between artists, I wanted to track “graffiti” artist’s affiliations with movements other than “graffiti.” There seems to be a range of nomenclature for graffiti artists, sometimes called “street” artists, sometimes “urban” artists, sometimes “vandals,” and I wanted to track the artistic lineage of these artists, tracing their influences in art movements to see how best one might situate graffiti in art history. The Gephi map and JS wrapper renders this network diagram in a browser.

Usage
===========
As with the graphitiTime and graphitiMap repos, my procedure for data cleaning and preparation as well as the stack detailed below could apply to other NYC gov datasets as accessed through socrata and visualized as a map. Preparing to rectify nyc data xy s to usable lat longs alone is worth a description.

Procedure
===========
### Data Mining and Cleaning ###
For data, I consulted Wikipedia for a list of Graffiti Artists; ultimately selecting a list of [“street artists” in Wikipedia](http://en.wikipedia.org/wiki/List_of_street_artists) and then pulling a larger list of “mural artists” from Freebase.  After investigating the analog of [“Street Artists” in DBpedia](http://dbpedia.org/page/List_of_street_artists), which allows users to run SPARQL queries across most all Wikipedia content and then export, I created an Excel table combining the known artists, art genre, affiliated movement, and location of origin across both the dbpedia list and the freebase collection. Some gaps in affiliated movements had me digging in the Wikipedia pages for references to movements, which were completed with at least one movement>artist pair per artist, often more. This resulted in a taxonomy of approximately 26 art movements as common references between the 170+ artists in the collection. Movements were non-discriminatory such that “mural art” and “street art” were among the accepted influence movements, with a hard stop on any reference to “graffiti.”
Thereafter, I split this reference table into an Edges table with a “Source” of movements matched to “Targets” of artists; those artists with multiple movements were listed more than once. I created a Nodes table with all of the entities (movements + artists) listed as IDs and matches to “Categories” of country locations for artists, and to the null value “movement” for art movements.

![Freebase](https://raw.github.com/auremoser/images/master/freebase.png)
![Nodes and Edges](https://raw.github.com/auremoser/images/master/nodes+edges.png)

### Visualization in Gephi ###
Loading the edges into Gephi, and then the nodes, adjusting the scatter/layout after loading with the Force Atlas 2, Force Atlas, Expansion, and Noverlap features to expand and fleshout the network and play with layouts. I then adjusted ranking of nodes (Ranking – OutDegree > Diamond Icon) to change the range size of nodes with more attached entities (min: 40, max: 60 , range 2-21), anticipating correctly that this would increase the size of the movements and maintain a smaller node size for unique entities (artists). I altered the color in the same dialog box, selecting a rainbow for all nodes according to the “Category” they were associated with, so nodes were colored by country, adding another layer of information to the graph, and allowing me to correspondingly color all nodes with the category “Movement” as grey (thus rendering all movements the same color). Pulling up the Preview Settings box, allowed me to adjust the opacity to 0, add text labels to replace all nodes (with the option “parent” which allows the labels to inherit color), and then adjust aesthetics to produce the below captioned PDF, and conduct analysis thereafter. Lastly, I created a key in Excel to serve as a country reference when considering the visualization.

![Gephi Nodes](https://raw.github.com/auremoser/images/master/final_nodes-gephi.png)
![Gephi Preview](https://raw.github.com/auremoser/images/master/final_vis-gephi.png)

### Gexf Visualization ###
Using the [gexf-js library](https://github.com/raphv/gexf-js), I pointed the config file to my own .gexf export and formated the diagram accordingly. In the process I lost some of the subtlety of the final gephi visualization :(. Adding a key to connect the colors to country indications as per the excel key created previously.

![Gexf Viz](https://raw.github.com/auremoser/images/master/graphNetgexf.png)

### Analysis ###
Broad conclusions about the project relate to the peculiar taxonomy of affiliated movements. As graffiti and street art developed a more substantial public art community, artists openly affiliate with more contemporary and less-formal art influences. The graffiti artists of today tend to identify with technique and are influenced primarily by situational circumstance: urban environments, political unrest/activism, and less by formalized art movements. Thus, “wheat-pasting,” “tattoo,” and “stencil art,” all focused on the more technical mechanics of art making become the dominant influences of this community. Principally self-taught, artists from non-western nations especially emphasize their debt to political situation, cultural colloquialisms, and urban landscape as motivations. Those art movements that are often referenced tend to follow this same program of motivations, with “street art” being tied to urbanism, “surrealism/dada” being tied to counterculture aesthetics, and “social realism” being tied to political activism. The imperative for independence, innovation, and resourcefulness can be read in the network of these influences.
While it would not be fair to assess this graph without acknowledging the limitations of my own manual data cleaning and simple data set, some generalizations such as the above seem fair. A glance at the graph reveals a complex but legible network of artists culled from countries on all continents, and a fair distribution for initial movement > graffiti artist relational studies.

![Final](https://raw.github.com/auremoser/images/master/final_vis-wide.png)


