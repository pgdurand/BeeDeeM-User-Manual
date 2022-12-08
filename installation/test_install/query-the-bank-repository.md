# Query the bank repository

### List installed banks

At any time, you can list installed banks as follows:

```
info.sh
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

### Query the BeeDeeM bank repository

You can also use [Utility tools](../../utils/) available with _BeeDeem_.

For instance, one of these tools is '[query](../../utils/cmdline-query.md)' which enables to query _BeeDeeM_ bank repository using sequence IDs. If you have succesfully installed _Human subdivision of Uniprot\_Swissprot_, as explained above, you can try this:

```
query.sh -d protein -i 1433S_HUMAN -f txt
```

```
Well, we hope that '1433S\_HUMAN' is still available in the Human Swissprot bank... if true, you'll see the full entry !
```

_Note_: during script execution, there is nothing displayed on the terminal whether something goes wrong. However, _BeeDeeM_ logs all its work in a dedicated log file located in _${workingDir}_.

Available formats in 'query.sh' command-line are: _txt_, _html_, _fas_, _insd_ and _finsd_.

[Read more about query tool](../../utils/cmdline-query.md).
