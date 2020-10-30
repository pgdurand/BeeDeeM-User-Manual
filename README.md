# Introduction

## Presentation

The Bioinformatics Databank Manager System \(called _BeeDeeM_\) is capable of installing on a local computing system major sequence databank file formats: **Genbank, Refseq, Embl, Genpept, Swissprot, TrEmbl, Fasta, Silva** and **BOLD**. In addition to sequence data files, _BeeDeeM_ can install major biological classifications \(ontologies\), such as **NCBI Taxonomy, Gene Ontology, Enzyme Commission and Intepro** **domains**. Plain text as well as compressed \(gzip\) and archived \(tar\) files are accepted by _BeeDeeM_.

Whatever the source of sequence files \(public institutes or personal data\), _BeeDeeM_ converts them into \(a\) BLAST databanks and \(b\) sequence data indexes. Then, all these databanks are available for use with several ready-to-use softwares and Java API \(see [Companion tools](./#companion-tools), below\).

The **conversion of sequence files into a BLAST databank** is done in a fully automated way by _BeeDeeM_. While NCBI 'makeblastdb' only handles Fasta files, _BeeDeeM_ is capable of converting directly Genbank, Refseq, Embl, Genpept, Swissprot, TrEmbl, Silva and BOLD files into a BLAST databank.

Sequence data indexes are used in various places of the software to **retrieve sequence annotations given sequence identifiers**. To achieve such a data retrieval task in a very effective way, the source sequence files have to come with a dictionary associating sequence identifiers to sequence data. Again, the Databank Manager is capable of creating such a dictionary automatically, whatever the format of the source sequence files.

Finally, concerning public sequence databanks, **the Databank Manager is capable of running in a fully automated way the retrieval of sequence files from the FTP servers of public institutes** \(such as NCBI, EBI, Uniprot, GeneOntology, _etc._\), as well as from your own in-house FTP servers if any are available.

## Main features

_BeeDeeM_ automatically performs:

* the download of the database files from remote sites \(via FTP\),
* the decompression of the files \(gzip files\),
* the un-archiving of the files \(tar files\),
* the conversion of native sequence banks \(e.g. Genbank\) to FASTA files,
* the preparation of databases in BLAST format from native sequence bank formats,
* the indexing of Genbank, Refseq, Embl, Genpept, Swissprot, TrEmbl, Fasta, Silva and BOLD files allowing their efficient querying by way of sequence identifiers,
* the indexing of sequence features and ontologies data \(NCBI Taxonomy, Gene Ontology, Enzyme Commission and Intepro domains\),
* the preparation of taxonomic subsets out of annotated sequence banks,
* the filtering of sequence banks with user-defined constraints.

## Main tools

_BeeDeeM_ provides a toolchain made of:

* [a command-line tool to automate databanks installation](getting-started/)
* [a UI front-end to do the same in a more friendly way](getting-started-1/)
* [a command-line tool to annotate BLAST results](utils/cmdline-annotate.md)
* [a command-line to query databanks using sequence IDs](utils/cmdline-query.md)

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

This manual explains how to install, configure and use _BeeDeeM_.

## License

_**BeeDeeM**_ **is a free open-source software** released under the terms of:

[![License AGPL](https://img.shields.io/badge/license-Affero%20GPL%203.0-blue.svg)](https://www.gnu.org/licenses/agpl-3.0.txt)

