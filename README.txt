FACETS : Multi-faceted Functional Decomposition of Protein Interaction 
Networks

Seah, Boon-siew
Bhowmick, Sourav S
Dewey, C Forbes

CONTACT:
seah0097@ntu.edu.sg or assourav@ntu.edu.sg

Bioinformatics. 2012 Oct 15;28(20):2624-31. doi: 10.1093/bioinformatics/bts469
##############################################################################################


FACETS requires Java 1.6 or above to execute. FACETS is free to use for non-commercial
purposes. Please execute as follows:

Running FACETS
##############################################################################################
1) Unzip the following files: out.zip, output.zip, gene_ontology2.1_0.obo.zip and gokeys_buf.zip

2) Create or obtain PSI-MI 2.5 XML formatted network PPI files (see IntAct: 
   www.ebi.ac.uk/intact/ for sample files). Note: PSI-MI 2.5 XML files outside
   IntAct may not have GO tags included. If that is the case, use the -a <go association file> 
   option to tag the proteins. You will need to obtain gp_association.goa_uniprot 
   from http://www.ebi.ac.uk/GOA/downloads.html. Tagging may take up to an hour.

   Alternatively, use sample FACETS .net input networks (human.net, for example). 
   FACETS will also create the .net version of PSI-MI networks when parsed.

3) Run with java -jar facets.jar <options> <network name>. It is recommended to run FACETS with
   the following JVM parameters (java -Xmx1024m -Xms32m -jar facets.jar <options> <network name>)
   (Example: java -Xmx1024m -Xms32m -jar facets.jar -n 6 human.net)


FACETS Options
################################################################################################

The following optional parameters are available:
  
-n <value> | --numFacets <value>
Specify number of facets (default = 6)

-m <value> | --minSize <value>
Minimum cluster size (default = 3)

-t <file> | --output type <file>
Output types (S = SIF files, T = Single file), default = S,T. When SIF files are
enabled, two types of Cytoscape viewable SIF (Simple Interaction File) files are 
generated. Each "all_" prefix SIF generate an entire subgraph for one facet, while
each "c_" prefix SIF is a subgraph for a single cluster.

When Single file output is enabled, a single "out_single.txt" file stores the 
FACETS output.

-a <GO association file> | --annotate <GO association file>
If your PSI-MI network is not tagged with GO information, annotate them using this 
option. You will need to obtain gp_association.goa_uniprot 
from http://www.ebi.ac.uk/GOA/downloads.html. Tagging may take up to an hour.

-d <file> | --output directory <file>
Output directory (default = .\output\)

-f <filter terms> | --filter <filter terms>
GO term hierarchies to consider (C = cellular component, S = cellular process, 
B = biological process, M = molecular function, default = C,S )
Specify which sub-DAG to include. Alternatively, you may specify the integer value of 
the GO IDs (100 for Translation). By default, only the Biological process sub-DAG is 
included. You can string together multiple sub-DAGs with commas, for example: -f S,B,M


Examples:
################################################################################################
1) Facets on human.net with 10 facets
java -jar facets.jar -n 10 human.net

2) Facets on human.net with 10 facets, no SIF output files
java -jar facets.jar -t T -n 10 human.net

3) Facets on human.net with 10 facets, no SIF output files, cellular process, molecular function
and cellular component 
java -jar facets.jar -f C,M,S -t T -n 10 human.net

4) PSI-MI XML
java -jar facets.jar -f C,M,S -t T -n 10 drome_small-01.xml


Analyzing FACETS out_single.txt
################################################################################################

The following columns will be generated:
Facet:  Facet number
Rank: Rank within facet based on this objective function score. 
Cluster: Cluster name. All proteins in this cluster shares this GO term. If fraction is shown, it 
represents the fraction of proteins in the cluster among all proteins annotated in the network
with that term.
GO ID: The shared GO ID.
Size: Number of proteins in cluster.	 
Members: Proteins in the cluster.



