# Databanks organization

## Organisation of directories housing the sequence databases

As indicated in the section [Directory structure](../installation/directory_structure.md), all databanks installed by _BeeDeeM_ are located in the directory _${biobaseDir}_.

If we use the example of the '**default.dg**' descriptor, the databank **PDB\_proteins**, **Uniprot\_Swissprot** and **Refseq\_Viruses** are installed into the directories described by their respective bank descriptor. If you look at these descriptors \(located in the directory _${conf}_\) and you look their directive _db.ldir_, this is what you will see:

| Descriptor | Installation instruction | Type | Bank name |
| :--- | :--- | :--- | :--- |
| _PDB\_proteins.dsc_ | db.ldir=${mirrordir} | p | PDB\_proteins |
| _Uniprot\_SwissProt.dsc_ | db.ldir=${mirrordir} | p | Uniprot\_SwissProt |
| _Refseq\_Viruses.dsc_ | db.ldir=${mirrordir} | n | Refseq\_Viruses |

All of these 'db.ldir', 'type' and 'bank name' directives translate into the following directory tree:

```text
${biobaseDir}
  |
  |- n
  |    |
  |    |- Refseq_Viruses
  |
  |      --> Contains Refseq_Viruses in flat-file annotated format, 
  |          a Lucene index, a FASTA version and the BLAST databank.
  | 
  |- p
       |
       |- Uniprot_SwissProt
       |    
       |   --> contains all data for Swiprot databank
       |
       |- PDB_proteins
```

It is worth noting that reserved descriptor keyword _${mirrordir}_ translates to _${biobaseDir}_ at runtime; see [Directory structure](../installation/directory_structure.md).

This example shows that in NO CASE the various databases are installed in the same directory. If this is not done, _BeeDeeM_ may malfunction, particularly during updates. In effect, if two databases are installed in the same directory, you cannot update them individually.

To install a new database, it is best to comply with the tree structure given above.

For example, if you wan to install the BLAST nucleic database 'MyBank', install it in its own directory under:

```text
${mirrordir}/n/MyBank.
```

In the same way, if you want to install the flat file proteic database 'MyOtherBank', install it in its own directory under:

```text
${mirrordir}/p/pMyOtherBank
```

## What to do after processing

When the installation of a sequence database was successful, it is automatically installed into production for your users.

The “old” copy of the database is always deleted, but this behaviour can be controlled using parameter 'history' of a databank descriptor.

Let's take the example from the database descriptor "test.dsc" located in the DDMS directory _${conf}_. Here, we are interested in two lines of this file:

```text
db.name=PDB_proteins
db.ldir=${mirrordir}|p|PDB_proteins
```

the first line gives the name of the database to install and the second line specifies where it should be installed on your system. Therefore, these two lines tell _BeeDeeM_ that the database [PDB](http://www.rcsb.org/pdb/home/home.do) \(sequences only\) will be installed in the directory ${mirrordir}\|p\|PDB\_proteins under the name PDB\_proteins.

When the processing of this database has succeeded, PDB\_proteins is installed into the following directory:

```text
${mirrordir}/p/PDB_proteins/current/PDB_proteins
```

Note the presence of the term _current_ in the path: it identifies the PDB\_proteins database currently in production, i.e. the version of the database used by your users.

Now let us suppose that you ask _BeeDeeM_ to update this database as of 26/02/2017. Throughout the processing of the database PDB, _BeeDeeM_ will work in a temporary directory named as follows:

```text
${mirrordir}/p/PDB_proteins/20170226/PDB_proteins
```

Note that the sub-directory 20170226 is at the same level as the sub-directory current \(see below\). This means that the database PDB\_proteins in production remains available \(and cohabits with\) the version being installed.

If the installation procedure ends successfully, the directories are renamed as follows ONLY is descriptor parameter 'history' is set to '1':

```text
${mirrordir}/p/PDB_proteins/current/PDB_proteins

becomes

${mirrordir}/p/PDB_proteins/currentOn20170226/PDB_proteins
```

\(the version that was in production migrates out of production\). If 'history' is set to '0', then the 'old' release of PDB\_proteins is automatically deleted.

If the installation procedure fails, these two directories are unchanged:

```text
${mirrordir}/p/PDB_proteins/current/PDB_proteins

and

${mirrordir}/p/PDB_proteins/20170226/PDB_proteins
```

In this case, you should consult the _BeeDeeM_ log files and search for the lines containing "WARN" \(refer to [Control of execution](install-banks/#control-of-execution) for more details\).

Each such "WARN" line contains the description of an error that occurred during processing. Once the problem has been identified, _BeeDeeM_ can be restarted: see section [Restart after failure](advanced-uses/#restart-after-failure).

