# Initial databank deployment

## Install a bank

Once installation is completed, you can run a test from the command-line as follows:

```
$ cd ${installDir}
$ ./install.sh swiss

where - ${installDir} should be replaced by the directory where BeeDeeM 
        is installed on your system 
      - 'swiss' is the name of the global descriptor to use to start
        bank installation (more on this later)
```

_Note_: during script execution, there is nothing displayed on the terminal whether something goes 'ok' or 'wrong'. However, _BeeDeeM_ logs all its work in a dedicated log file located in _${workingDir}_.

Once execution finishes, check the contents of the _BeeDeeM_ log file.

```
$ cat ${workingDir}/dbms-swiss.log | grep WARN

where ${workingDir} should be replaced by the working directory of BeeDeeM
```

If there are some WARN lines in the logs, then refer to the section [Appendix – Common errors](/cmdline/common-errors.md).

Otherwise, it means the annotated _Human subdivision of Uniprot\_Swissprot_ is now install on your system.

## Start working with BeeDeeM

### List installed banks

At any time, you can list installed banks as follows:

```
$ cd ${installDir}
$ ./info.sh

where - ${installDir} should be replaced by the directory where BeeDeeM 
        is installed on your system
```

Which gives you on the standard output:

```
BeeDeeM - 4.1.0

Configuration:

  Install path           : /opt/beedeem/
  Master configuration   : /opt/conf/dbms.config
  Log path               : /var/log/
  Work path              : /tmp/
  Bank configuration file: /biobase/dbmirror.config
  Bank repository path   : /biobase/
  Bank repository size   : 361,67 Mb

Installed banks
 - Protein banks: 1
      * SwissProt_human
        Description: Human subset of UniprotKB/SwissProt.
        BLAST+ use: -db /biobase/p/SwissProt_human/current/SwissProt_human/SwissProt_humanM
        Annotated bank: true
        Size (sequences): 20,168
        Size on disk: 361,67 Mb
        Install date: 2017-03-12, 17:55

 - Nucleotide banks: 0

 - Biological classification banks: 0
```

### Install more databanks

If the preceeding test was successful, you can continue to install some databanks:

* from the command-line, jump to [CmdLineInstaller](/cmdline/getting-started.md)
* from the graphical interface, jump to [UiInstaller](/ui/getting-started.md)

### Query the BeeDeeM bank repository

You can also use [Utility tools](/utility/utils.md) available with _BeeDeem_.

For instance, one of these tools is '[query](/utility/cmdline-query.md)' which enables to query _BeeDeeM_ bank repository using sequence IDs. If you have succesfully installed _Human subdivision of Uniprot\_Swissprot_, as explained above, you can try this:

```
$ cd ${installDir}
$ ./query.sh -d protein -i 1433S_HUMAN -f txt
```

```
Well, we hope that '1433S\_HUMAN' is still available in the Human Swissprot bank... if true, you'll see the full entry !
```

_Note_: during script execution, there is nothing displayed on the terminal whether something goes wrong. However, _BeeDeeM_ logs all its work in a dedicated log file located in _${workingDir}_.

Available formats in 'query.sh' command-line are: _txt_, _html_, _fas_, _insd_ and _finsd_.

[Read more about query tool](/utility/cmdline-query.md).

### Run a BLAST search

_Note:_ we suppose that NCBI BLAST+ software is installed on you computer.

_BeeDeeM_ creates a BLAST databank for every sequence databank installed.

So, you can easily run BLAST jobs, as illustrated by this command-line snippet:

```
# We get a query sequence from BeeDeeM repository
$ ./query.sh -d protein -i 1433S_HUMAN -f fas > 1433S_HUMAN.fas

# We "BLASTp" that query against the installed Human subdivision of Uniprot_Swissprot
$ blastp -db /biobase/p/SwissProt_human/current/SwissProt_human/SwissProt_humanM \
         -query 1433S_HUMAN.fas -outfmt 5 -out 1433S_HUMAN.blastp
```

In turn, the BLAST result file \(1433S\_HUMAN.blastp\) can be viewed using the [BLAST Viewer software](https://github.com/pgdurand/BlastViewer).

[Read more](/utility/run-blast.md) about using BLAST with BeeDeeM-managed banks.

### Annotate a BLAST result

Let us terminate this mini-tutorial with another feature of BeeDeeM: its capability of introducing Features Table data into BLAST result files.

**How this feature is possible? **

Only if the target databank contains features. A simple FASTA file does not contain such information. However, banks from Uniprot or Genbank do contain such information.

Ok, try this on the command-line:

```
$ cd ${installDir}
$ ./query.sh -d protein -i 1433S_HUMAN -f txt
```

Among the many types of information, that Swissprot entry contains:

```
OX   NCBI_TaxID=9606;
.../...
DR   GO; GO:0005913; C:cell-cell adherens junction; IDA:BHF-UCL.
DR   GO; GO:0005737; C:cytoplasm; IDA:HPA.
DR   GO; GO:0030659; C:cytoplasmic vesicle membrane; TAS:Reactome.
.../...
DR   InterPro; IPR000308; 14-3-3.
DR   InterPro; IPR023409; 14-3-3_CS.
DR   InterPro; IPR023410; 14-3-3_domain.
.../...
FT   CHAIN         1    248       14-3-3 protein sigma.
FT                                /FTId=PRO_0000058643.
FT   SITE         56     56       Interaction with phosphoserine on
FT                                interacting protein.
```

These are: taxonomy ID \(OX line\), GeneOntology and InterPro ontology IDs \(DR lines\) and a Features Table \(FT lines\).

**Let's annotate a BLAST result!**

Now, you can annotate a BLAST result as follows \(we resume the above example where we produce the BLAST file: 1433S\_HUMAN.blastp\):

```
$ cd ${installDir}
./annotate.sh -i 1433S_HUMAN.blastp -o 1433S_HUMAN.zml -type full -writer zml
```

_Note_: during script execution, there is nothing displayed on the terminal whether something goes wrong. However, _BeeDeeM_ logs all its work in a dedicated log file located in _${workingDir}_.

A 'zml' file is a dedicated zip-compressed XML format capable of representing what we call a [Rich Search Result](https://github.com/pgdurand/Bioinformatics-Core-API/tree/master/src/bzh/plealog/bioinfo/api/data/searchresult), i.e. a BLAST data model augmented with Features \(standard NCBI BLAST XML format is not capable of doing that\).

You can analyze the content of '1433S\_HUMAN.zml' using the [BLAST Viewer software](https://github.com/pgdurand/BlastViewer) or by writing your own home-made tool using the [Bioinformatics Core API](https://github.com/pgdurand/Bioinformatics-Core-API).

[Read more](/utility/cmdline-annotate.md) about annotating BLAST results with BeeDeeM-managed banks.

