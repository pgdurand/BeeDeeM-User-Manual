# Query the bank repository

### List installed banks

At any time, you can list installed banks as follows:

```
bdm info -d all -f txt
```

Which gives you on the standard output:

```
BeeDeeM - 5.5.0

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

All banks installed by BeeDeeM can be searched for by entry ID using the bdm query command, such as:

```
bdm query -d protein -i 1433S_HUMAN -f fas
```

Available formats for `bdm query` command-line are: _txt_, _html_, _fas_, _insd_ and _finsd_.

[Read more about query tool](../../utils/cmdline-query.md).
