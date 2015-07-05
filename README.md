# S.PhyloMaker
This repository includes four files: R_codes for S.PhyloMaker, PhytoPhylo, nodes, and example.splist, in addition to the Readme file. Below are descriptions for each of these files.

1. R_codes for S.PhyloMaker    
    S.PhyloMaker is a function that generates phylogenies for seed plants. (Note: Before running this function, please install and load the "phytools" package.)

  1.1 Description    
    This R function (i.e., S.PhyloMaker) generates phylogenies for seed plants under three scenarios, which are described in the paper. This function should be used in conjunction with PhytoPhylo, a megaphylogeny for vascular plants. 

  1.2 Usage    
    S.PhyloMaker(splist, tree, nodes, output.splist = T, scenarios = c("S1", "S2", "S3"))

  1.3 Arguments    
    splist: a user specified data frame which contains a list of seed plant species for which S.PhyloMaker generates phylogenies. This data frame should include three columns with field names of species, genus, and family. The three columns are, respectively, for species name (e.g. Acacia berlandieri), genus name (e.g. Acacia), and family name (e.g. Fabaceae). 

    tree: a phylo object; the megaphylogeny of vascular plants (i.e. PhytoPhylo). 

    nodes: a data.frame; it contains the basal node information of every family and genus on the megaphylogeny (i.e. PhytoPhylo).

    output.splist: logical; the output includes the columns of the "splist" data frame and an extra column showing which species in "splist" have matched with species in the megaphylogeny. 

    scenarios: optional; defining which scenario(s) will be used to generate phylogenies. By default, three phylogenies corresponding to the three scenarios are generated. 

  1.4 Details    
    Using the PhytoPhylo megaphylogeny as a backbone, this function takes a user-specified species list and matches species in the species list with species in the megaphylogeny. If a species is found in the megaphylogeny, the species will be selected for pruning; if the species is not found but its genus or family is found in the megaphylogeny, the species will be added to the backbone at a certain place within the genus or family depending on which scenarios are taken. Finally, the selected and added species are pruned from the megaphylogeny, which results in three phylogenies corresponding to the three scenarios (when default is chosen). 

  1.5 Value    
    The output of a run on the function contains a set of three phylogenies corresponding to the three scenarios (when default is chosen) and a species list, which includes the original columns of the "spList" data frame and an additional column (called "status") showing which species in the user’s species list have matched with species in the megaphylogeny. Species matched between the species list and the megaphylogeny are indicated as "match(prune)"; species that are added to the megaphylogeny before the pruning are indicated as "match(add)"; species whose genera or families are not found in the megaphylogeny are indicated as "unmatch". 

  1.6 Example   
    library("phytools")                       # load the "phytools" package.
    example<-read.csv("example.splist.csv",header=T)       # read in the example species list.
    phylo<-read.tree("PhytoPhylo.tre")      # read in the megaphylogeny.
    nodes<-read.csv("nodes.csv",header=T)     # read in the nodes information of the megaphylogeny.
    result<-S.PhyloMaker(splist=example, tree=phylo, nodes=nodes)      # run the function S.PhyloMaker.
    str(result)       # the structure of the ouput of S.PhyloMaker.
    par(mfrow=c(1,3),mar=c(0,0,1,0))       # show the phylogenies of the three scenarios.
    plot(result$Scenario.1,cex=1.1,main="Scenarion One")
    plot(result$Scenario.2,cex=1.1,main="Scenarion Two")
    plot(result$Scenario.3,cex=1.1,main="Scenarion Three")

2. PhytoPhylo    
    This is the megaphylogeny that is used as the backbone for S.PhyloMaker to generate phylogenies. The content of PhytoPhylo is also included in Appendix S3.

3. nodes    
    This is the data frame that contains the information of the basal node information of every family and genus on the megaphylogeny (i.e. Phytophylo), as described in the “nodes” subsection of section 1.3.

4. example.splist    
    This is an example of species list on which S.PhyloMaker can run. It includes three columns, which are species, genus and family names. 


