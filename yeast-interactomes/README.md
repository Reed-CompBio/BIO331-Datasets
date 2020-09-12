# Yeast interactomes

These undirected, unweighted interactomes come from two sources: the Yu et al. 2008 paper and BioGRID.

## Yu et al., 2008

The following paper describes three interactomes: a Yeast-Two-Hybrid network, an AP/MS network, and a literature curated network.

Yu H, Braun P, Yildirim MA, et al. [High-quality binary protein interaction map of the yeast interactome network](https://pubmed.ncbi.nlm.nih.gov/18719252/). Science. 2008;322(5898):104-110.

The data is available from Harvard's [Yeast Interaction Database](http://interactome.dfci.harvard.edu/S_cerevisiae/), and are downloaded from their [downloads page](http://interactome.dfci.harvard.edu/S_cerevisiae/index.php?page=download):

- `Yeast_Y2H_Union.txt` - union of three screens from [Yu et al.](https://pubmed.ncbi.nlm.nih.gov/18719252/)
- `Yeast_Combined_APMS.txt` - co-complex membership interactions from [Collins et al.](http://www.ncbi.nlm.nih.gov/pubmed/17200106)
- `Yeast_LC_Multiple.txt` - literature-curated interactions from [Reguly et al.](http://www.ncbi.nlm.nih.gov/pubmed/16762047)

## BioGRID

The [Biological General Repository for Interaction Datasets (BioGRID)](https://thebiogrid.org/) contains protein  for dozens of organisms.  The data is available from their [downloads page](https://downloads.thebiogrid.org/BioGRID) and subsetted to produce the following datasets:

- `BioGRID_physical.txt` - all unique physical interactions reported in BioGRID.
- `BioGRID_Y2H.txt` - all unique [two-hybrid](https://wiki.thebiogrid.org/doku.php/experimental_systems) interactions reported in BioGRID.
- `BioGRID_APMS.txt` - all unique [affinity capture-MS](https://wiki.thebiogrid.org/doku.php/experimental_systems) interactions reported in BioGRID.

These datasets only include proteins with systematic names and were generated 9/13/2020 with v0.189.  From the [tab3 format](https://wiki.thebiogrid.org/doku.php/biogrid_tab_version_3.0), let `BIOGRID.tab3.txt` be the downloaded _S. cerevisiae_ file.

```
awk -F "\t" '($13=="physical" && $6!="-" && $7!="-" ){print $6"\t"$7}' BIOGRID.tab3.txt | sort | uniq > BioGRID_physical.txt
awk -F "\t" '($12=="Two-hybrid" && $6!="-" && $7!="-" ){print $6"\t"$7}' BIOGRID.tab3.txt | sort | uniq > BioGRID_Y2H.txt
awk -F "\t" '($12=="Affinity Capture-MS" && $6!="-" && $7!="-" ){print $6"\t"$7}' BIOGRID.tab3.txt | sort | uniq > BioGRID_APMS.txt
```
