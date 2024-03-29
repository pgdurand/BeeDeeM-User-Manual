# List installed banks

_BeeDeeM_ comes with an additional tool aims at listing installed banks.

This tool also helps you to locate:

* banks that are available for use with BLAST software
* banks containg annotations

The tool is only available from the command line and is called:

* bdm info -h

_Note:_ during script execution, there is nothing displayed on the terminal whether something goes OK or wrong. However, _BeeDeeM_ logs all its work in a dedicated log file located in ${workingDir}. Refer to [Directory structure](../installation/directory\_structure.md) for more information.

## Command-line use

Command line takes no arguments. Simply use:

```
bdm info -d all -f txt
```

The result is directly dumped in standard output, such as:

```
BeeDeeM - 5.0.0

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

The 'info' command accepts the following optional arguments:

```
-d <type-of-repository> -f <format> -u <username>
```

where:

* "type-of-repository" is one of: n, p, b, all. This allows you to list nucleotide, protein, biological calssifications or all banks, respectively. Default is: all.
* "format" is one of: txt, html, galaxy. Default is: txt.

You can control `bdm info` tool with some environment variables as stated [in this section](../getting-started/beedeem-configuration.md).&#x20;

## Locate your BLAST banks

Using that utility tool, you can easily identify banks that are available for BLAST. If you have a closer look at the above bank list, you will see this line:

```
BLAST+ use: -db /biobase/p/SwissProt_human/current/SwissProt_human/SwissProt_humanM
```

This is the "-db" argument you can use with BLAST+ software to run a BLAST job against that bank.

## Locate banks to annotate your BLAST results

In a same way, the above output displays that line:

```
Annotated bank: true
```

Which means that the "SwissProt\_human" contains annotations: features and biological classifications. So, that bank can be used with the [Annotate tool](cmdline-annotate.md).

## Get loc files for Galaxy

You can easily enable Galaxy web platform to use banks installed by BeeDeeM by creating loc files as follows:

```
# dump nucleotide banks into appropriate loc file
bdm info -f galaxy -d n > blastdb_n.loc

# do the same for protein banks
bdm info -f galaxy -d p > blastdb_p.loc
```

Such files contains list of banks ready to be used by NCBI BLAST Galaxy wrappers.
