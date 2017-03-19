# Annotate BLAST results

*BeeDeeM* comes with an additional tool aims at annotating BLAST results. This annotation processing means to introduce features data within each HSP contained in a BLAST results. That information is, of course, retrieved from the databanks managed by *BeeDeeM*.

That tool is only available from the command line and is called:

* annotate.sh: to be used on Linux or Mac OSX system
* annotate.bat: to be used on Windows system

*Note:* during script execution, there is nothing displayed on the terminal whether something goes OK or wrong. However, *BeeDeeM* logs all its work in a dedicated log file located in ${workingDir}. Refer to [Directory structure](/directory_structure.md) for more information.

## Requirements

* BLAST searches have to be done against BLAST databanks prepared by *BeeDeeM*;

* use either legacy BLAST or BLAST+ software;

* set BLAST program to produce results formatted as legacy XML.

## What is a legacy BLAST XML result file?

A legacy NCBI XML BLAST file is the result file you create when using the following argument of BLAST+:

    -outfmt 5 

For those of you that are still using the legacy BLAST (_i.e. blastall_), use this argument:

    -m 7



## Command-line use

Command line takes three arguments, in this order:

    <BLAST result> <output file> <type>

* **BLAST result** \[_required_\]: input BLAST file that has to be annotated \(absolute path\); must be legacy BLAST XML formatted; 
* **output file** \[_required_\]: output file that will contain the annotated BLAST result \(absolute path\); 
* **type** \[_required_\]: type of annotation to retrieve. Use one of: bco or full. Use "bco" to only retrieve biological classifications information. Use "full" to retrieve full feature tables.

[Sample use case](/test_install.md#annotate-a-blast-result).

In addition, some parameters can be passed to the JVM for special configuration purposes:

* -DKL\_DEBUG=true ; if true, log will be in debug mode
* -DKL\_WORKING\_DIR=an\_absolute\_path ; if not set, log and working directories are set to java.io.tmp
* -DKL\_LOG\_FILE=a\_file\_name ; if set, creates a log file with that name within KL\_WORKING\_DIR

## Output format

This program produces an output file using a dedicated format that can represent a BLAST results containing Feature Tables \(original BLAST XML format does not handle that\).

In turn, such files can only be handled using:

* [BLAST Viewer](https://github.com/pgdurand/BlastViewer) tool
* [BLAST Filter](https://github.com/pgdurand/BLAST-Filter-Tool) Tool
* [Plealog Bioinformatics Core API](https://github.com/pgdurand/BeeDeeM/wiki/Explore-annotated-BLAST-results)

The two former tools provide you with ready-to-use softwares to view and analyze annotated BLAST result files. The latter enables you to write your own Java-based tool to deal with such files in a convenient way. [More here](https://github.com/pgdurand/BeeDeeM/wiki/Explore-annotated-BLAST-results).

