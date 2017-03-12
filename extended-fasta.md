# *BeeDeeM* extended FASTA formatWhen a BLAST databank is created from Genbank, Refseq, Embl, Genpept, Swissprot or TrEmbl formatted files, *BeeDeeM* will use an extended procedure to inject classification data (NCBI Taxonomy, GeneOntology, Interpro, Pfam and EC) directly into the BLAST databank. In that way, every search job using BLAST will create BLAST results containing classification data. It is worth noting that biological classifications have to be installed for a correct use of this *BeeDeeM* extended feature.
## Preparing personal Fasta files with classification data
The *BeeDeeM* extended feature mentioned in the previous section can be used with your personal Fasta files. 
For that purpose, you have to set specific Fasta headers for the sequences available in the file.
A standard Fasta header is as follows:    >3BHS1_MACMU dehydrogenaseA *BeeDeeM* extended Fasta header is as follows:
    >3BHS1_MACMU dehydrogenase [[taxon:9544;EC:1.1.1.145,5.3.3.1;GO:0005789]]
    As you can see, *BeeDeeM* accepts additional data at the end of the Fasta header and within two double square brackets. For now, the only accepted additional data is made of cross-reference IDs to the following classifications: NCBI Taxonomy, GeneOntology, Interpro, Pfam and EC. 
The general format of the string to place between [[ and ]] is: db:id. 
* 'db' must be one of: taxon, GO, Pfam, Interpro and EC (these keys are case-sensitive);
* 'id' is an identifier. 
For GeneOntology and Enzyme Commission, do not prefix id with the term GO and EC, respectively (see above example). 
When several identifiers are available for a same classification, use a comma to separate them. Here is an example:    [[taxon:9544;EC:1.1.1.145,5.3.3.1;GO:0005789,0016021;Pfam:PF01073;InterPro:IPR002225,IPR016040]]