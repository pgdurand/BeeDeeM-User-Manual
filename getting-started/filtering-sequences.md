# Filter sequences

When using indexing tasks \(idxem, idxsw, idxgb, idxgp or idxfas; see [Unit tasks](descriptors-format.md#unit-tasks)\), specific parameters are available to retain or discard sequences from source files.

Theses parameters allow:

* to cut a sequence file by sequence rank numbering
* to filter a sequence file by sequence size
* to filter a sequence file by sequence description

## Cut source files

The new parameter 'cut' requires two values separated by the keyword 'to': the first and the last sequence rank number identifying sequences to keep from the source sequence file. The value '-1' means no limit.

Examples:

* cut=10to1000 : instructs KDMS to keep 990 sequences ranked 10th to 1000th in the source file
* cut=-1to500 : keep the 500 first sequences
* cut=30to-1 : discard the 29 first sequences

## Filter by sequence size

The parameter 'seqsize' requires two values separated by the keyword 'to' : the minimum size and the maximum size of the sequences to keep from the source sequence file. The value '-1' means no limit.

Examples:

* seqsize=20to50 : keep only sequences containing more than 19 letters and less than 51
* seqsize=-1to100 : keep only sequences containing less than 101 letters
* seqsize=50to-1 : keep only sequences containing more than 51 letters

## Filter by sequence description

A sequence description may contain a lot of terms. The parameter 'desc' allows filtering to keep or discard some terms provided in a sequence description.

By default, the filter engine considers the terms exactly spelled. If you want to enable misspelling, use option 'exactdesc' set to 'false' \(see example, below\).

Multiple terms have to be separated by '@'. Terms to discard have to be prefixed with '!'.

Examples:

* desc=kinase : keep sequences containing the term 'kinaze' in their description
* desc=kinaze;exactdesc=false : keep sequences containing a word approaching 'kinaze' in their description
* desc=maturasse@kinasse;exactdesc=false : keep all sequences containing a word approaching 'kinasse' OR 'maturase' in their description
* desc=!kinase : discard sequences containing 'kinaze' in their description
* desc=kinase@!maturase : keep sequences containing 'kinase' but not 'maturase' in their description

All these parameters have be added in the indexing task: idxem, idxsw, idxgb, idxgp and idxfas.

Example for a Fasta file:

* idxfas\(cut=-1to1000;seqsize=200to300;desc=maturose@kanise@!isolatus;exactdesc=false\)

## Prepare a taxonomic specific data subset

In the above mentioned tables, some tasks accept taxonomic constraints; these arguments are 'taxinc' and 'taxexc'.

Both of them accept a comma separated list of taxon IDs that will be used to retain \(taxinc\) or discard \(taxexc\) taxonomic-specific sequences.

Only NCBI taxonomic numeric ID are accepted \(e.g. for _Homo sapiens_, use ID 9606\). The use of these constraints only apply for sequence data files containing taxonomic data \(Genbank, Refseq, Embl, Genpept, Swissprot, TrEmbl\). Source sequences having no taxonomic information are always kept for inclusion in sequence annotation and Blast databanks.

