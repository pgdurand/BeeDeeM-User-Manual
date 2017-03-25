# Install databanks


## Install public databanks

Within the Databanks Sources panel, select the tab called Public Databanks. There, you can see a list of pre-configured databank descriptors.







































## Prepare taxonomic specific data subsets

The panel Install Personal Databanks enables you to prepare taxonomic specific data subsets. For that purpose, use one or the two fields called 'Include taxons' and 'Exclude taxons'. Both of them accept a comma separated list of taxon IDs that will be used to retain (include taxons) or discard (exclude taxons) taxonomic-specific sequences. Only NCBI taxonomic numeric ID are accepted (e.g. for Homo sapiens, use ID 9606). The use of these constraints only apply for sequence data files containing taxonomic data (Genbank, Refseq, Embl, Genpept, Swissprot, TrEmbl). Source sequences having no taxonomic information are always kept for inclusion in sequence annotation and Blast databanks.