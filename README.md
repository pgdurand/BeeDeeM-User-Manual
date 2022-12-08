# Introduction

## Presentation

BeeDeeM is a general-purpose Bioinformatics Databank Manager.&#x20;

This manual explains how to install, configure and use _BeeDeeM_.

## Main features

_BeeDeeM_ automatically performs:

* the handling of any set of files compliant to Genbank, Refseq, Embl, Genpept, Swissprot, TrEmbl, Fasta and Silva formats&#x20;
* the handling of major biological classifications (ontologies), such as NCBI Taxonomy, Gene Ontology, Enzyme, Intepro and PFAM&#x20;
* the download of files from remote sites (via FTP or Aspera),
* the decompression of the files (gzip files),
* the un-archiving of the files (tar files),
* the conversion of native sequence banks (e.g. Genbank) to FASTA files,
* the preparation of databanks in BLAST format from native sequence bank formats,
* the indexing of Genbank, Refseq, Embl, Genpept, Swissprot, TrEmbl, Fasta and Silva files allowing their efficient querying by way of sequence identifiers,
* the indexing of sequence features and ontologies data (NCBI Taxonomy, Gene Ontology, Enzyme Commission, Intepro and PFAM domains),
* the preparation of taxonomic subsets out of annotated sequence banks,
* the filtering of sequence banks with user-defined constraints.

_Task execution extension:_

* Any kind of pre- and post-processing of data can be done using external scripts
* Such scripts can be executed on the host computer (local mode) or though SGE, PBS or SLURM scheduler (cluster mode)
* Task executions are controlled by configuration files; _e.g._ to specify software ressources (RAM, CPU, walltime), access to softwares (direct execution or through Conda), _etc._

_Index creation extension:_

* Using the task execution engine, additional index can be quite easily created in a fully automated way (e.g. Diamond, Bowtie, _etc._)&#x20;

## Main tools

_BeeDeeM_ provides a toolchain made of:

* [a command-line tool to automate databanks installation](getting-started/)
* [a command-line tool to annotate BLAST results](utils/cmdline-annotate.md)
* [a command-line to query databanks using sequence IDs](utils/cmdline-query.md)
* [a UI front-end to do the same in a more friendly way](getting-started-1/)

## Practical use cases

Among others, these databanks can be used to:

* prepare and maintain up-to-date local copy of usefull data
* run BLAST sequence comparison jobs
* annotate BLAST results with sequence features and ontologies

## Companion tools

_BeeDeeM_ features and data are accessible from:

* [BioDocument Viewer](https://github.com/pgdurand/BioDocumentViewer)
* [BLAST Viewer](https://github.com/pgdurand/BlastViewer)
* [BLAST Filter Tool](https://github.com/pgdurand/BLAST-Filter-Tool)
* [Plealog Bioinformatics Core API](https://github.com/pgdurand/Bioinformatics-Core-API)

## More about some features

### Ready for cluster

BeeDeeM can be used from the command-line or from a graphical user interface. It is cluster ready: use of a job scheduler (e.g. PBS, SLURM), smooth use of cluster structures (e.g. data downloading from Internet-connected nodes vs. data processing on network-isolated nodes).&#x20;

### Ready for Aspera

BeeDeeM is capable of using the Aspera high speed data transfer system. In such a way, the software can quickly retrieve data from NCBI and EBI, both institutes providing Aspera servers for data retrieval.

### Annotate your BLAST results

The software comes with utility tools such as databank filtering, databank querying, and BLAST/DIAMOND/PLAST annotator; banks installed by BeeDeeM being indexed, they can be used to collect features data (including ontologies) and add all that information within results of above mentioned sequence comparison tools.

### Parallel data processing engine

Whatever the source of sequence files (public institutes or personal data), _BeeDeeM_ converts them into (a) BLAST databanks and (b) sequence data indexes. Then, all these databanks are available for use with several ready-to-use softwares and Java API (see [Companion tools](./#companion-tools)).

The conversion of sequence files into a BLAST databank is done in a fully automated way by _BeeDeeM_. While NCBI 'makeblastdb' only handles Fasta files, _BeeDeeM_ is capable of converting directly Genbank, Refseq, Embl, Genpept, Swissprot, TrEmbl and Silva files into a BLAST databank in avery straightforward way.

Sequence data indexes are used in various places of the software to retrieve sequence annotations given sequence identifiers. To achieve such a data retrieval task in a very effective way, the source sequence files have to come with a dictionary associating sequence identifiers to sequence data. Again, the Databank Manager is capable of creating such a dictionary automatically, whatever the format of the source sequence files.

Finally, concerning public sequence databanks, BeeDeeM is capable of running in a fully automated way the retrieval of sequence files from the FTP servers of public institutes (such as NCBI, EBI, Uniprot, GeneOntology, _etc._), as well as from your own in-house FTP servers if any are available.

## License

_**BeeDeeM**_** is a free open-source software** released under the terms of:

[![License AGPL](https://img.shields.io/badge/license-Affero%20GPL%203.0-blue.svg)](https://www.gnu.org/licenses/agpl-3.0.txt)
