# Annotate BLAST results

_BeeDeeM_ comes with an additional tool aims at annotating BLAST results. This annotation processing means to introduce features data within each HSP contained in a BLAST result. That information is, of course, retrieved from the databanks managed by _BeeDeeM_.

That tool is only available from the command line and is called:

* bdm annot -h

_Note:_ during script execution, there is nothing displayed on the terminal whether something goes OK or wrong. However, _BeeDeeM_ logs all its work in a dedicated log file located in ${workingDir}. Refer to [Directory structure](../installation/directory\_structure.md) for more information.

## Annotation explained

"Annotating" a BLAST result means adding two types of information to the XML BLAST result files :

* Ontology data, namely IDs and descriptions from Gene Ontology, Enzyme, InterPro, PFAM or NCBI Taxonomy, if any are available in the reference bank;
* Feature tables located on matching regions of hits.

**How all of these can happen?**

First of all, you have to understand that during the installation of a bank, either a sequence one (e.g. SwissProt) or an ontology one (e.g. Gene Ontology), BeeDeeM prepares data into dedicated indexes as illustrated here:

![](../.gitbook/assets/beedeem-indexer.png)

Then, you have to understand that a BLAST XML file produced from a BLAST bank prepared by BeeDeeM contains both Hits IDs **and** Ontology IDs. BeeDeeM annotator will be capable of using all these IDs to gather very useful data from sequence and ontology banks installed by BeeDeeM, too.

Finally, you have to know that BeeDeeM provides two types of "annotation" processing: **BCO** or **Full**, as illustrated here:

![](../.gitbook/assets/beedeem-BCO-annotator.png)

![](../.gitbook/assets/beedeem-FULL-annotator.png)

## Requirements to use BeeDeeM Annotator

* BLAST searches have to be done against BLAST databanks prepared by _BeeDeeM_; use the [info](list-banks.md) tool to list BLAST banks that also contains annotations;
* use either legacy BLAST or BLAST+ software;
* set BLAST program to produce results formatted as XML (legacy or XML2).

## How to produce a BLAST XML result file?

For instance, you can produce a legacy NCBI XML BLAST file using the following argument of BLAST+:

```
-outfmt 5
```

For those of you that are still using the legacy BLAST (_i.e. blastall_), use this argument:

```
-m 7
```

## Command-line use

Command line takes three arguments, in this order:

```
bdm annot -i <BLAST result> -o <output file> -type <type> -writer <writer>
```

* **BLAST result** \[_required_]: input BLAST file that has to be annotated (absolute path); must be legacy BLAST XML formatted;&#x20;
* **output file** \[_required_]: output file that will contain the annotated BLAST result (absolute path);&#x20;
* **type** \[_required_]: type of annotation to retrieve. Use one of: bco or full. Use "bco" to only retrieve biological classifications information. Use "full" to retrieve full feature tables.
* **writer** \[_required_]: writing format. Use one of: xml or zml. Use zml to save feactures and classification data. Use xml to save using NCBI legacy XML format.

Run program "bdm annot -h" to review command-line usage.

[Sample use case](../installation/test\_install/#annotate-a-blast-result).

You can control `bdm annot` tool with some environment variables as stated [in this section](../getting-started/beedeem-configuration.md).&#x20;

## Output format

This program produces an output file using a dedicated format that can represent a BLAST results containing Feature Tables (original BLAST XML format does not handle that).

In turn, such files can only be handled using:

* [BLAST Viewer](https://github.com/pgdurand/BlastViewer) tool
* [BLAST Filter](https://github.com/pgdurand/BLAST-Filter-Tool) Tool
* [Plealog Bioinformatics Core API](https://github.com/pgdurand/BeeDeeM/wiki/Explore-annotated-BLAST-results)

The two former tools provide you with ready-to-use softwares to view and analyze annotated BLAST result files. The latter enables you to write your own Java-based tool to deal with such files in a convenient way. [More here](https://github.com/pgdurand/BeeDeeM/wiki/Explore-annotated-BLAST-results).

## List annotated banks

Use the [info](list-banks.md) tool to list banks that contains annotations.
