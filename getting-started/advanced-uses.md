# Advanced uses

## Restart after failure

When processing fails, no sequence database being processed is put into production and the databases currently in production are not modified. Once the problem has been identified and resolved (_c.f._ [Control of execution](install-banks.md#control-of-execution)), _BeeDeeM_ can be restarted. It will analyse what was already done with success to install a particular bank, then it will resume remaing tasks.

## Processing of a specific database

A global descriptor file allows custom processing of the databases: either one database at a time or several databases simultaneously. In particular, this possibility is provided because the update frequency of the various sequence databases varies from one database to another.

For example, the file 'default.gd' located in the directory _${installDir}/conf/descriptors_ gives _BeeDeeM_ the instructions to process three databases. This instruction is given by the line 'db.list' in the global descriptor file.

Let's take this example: we only want to update Swissprot database. To just process this database, start by making a copy of the file default.gd:

```
$ cd ${installDir}/conf/descriptors
$ cp default.gd swOnly.gd
```

Edit the file 'swOnly.gd' to have the following line correctly configured:

```
db.list=Uniprot_SwissProt
```

The term 'Uniprot\_SwissProt' refers to the database descriptor file (without its ".dsc" extension) which must exist in the directory _${conf}_.

Do not forget to set up the "resume.date" line in the global descriptor as follows:

```
resume.date=none
```

before starting _BeeDeeM_.

Once the global descriptor is edited, you can start the processing:

```
bdm install swOnly
```

An alternative to that solution (copy a global descriptor, then edit that copy) would be to simply do:

`bdm install -desc Uniprot_SwissProt`

## Knowing disk space required for a databank

It is often useful to know how much disk space will be used by a sequence database. _BeeDeeM_ can simply answer this question, as explained below.

We will use the example of the global descriptor file 'default.gd' located in the directory _${installDir}/conf/descriptors_. Open the file and find the following line:

```
db.main.task=download
```

This line tells _BeeDeeM_ to download and install the databases. If you change this line to:

```
db.main.task=info
```

you tell _BeeDeeM_ that it should just give you a list of the files that it will download and their size.

To try this out, copy the file 'default.gd' to 'dataSize.gd', modify this copy as shown above (db.main.task=info) and start the processing:

```
$ cd ${installDir}/conf/descriptors
$ cp default.gd dataSize.gd

(edit dataSize.gd to replace line 'db.main.task=download' by 'db.main.task=info')
(save the file)

bdm install dataSize 

where ${installDir} should be replaced by the directory where BeeDeeM is installed on your system).
```

Once _BeeDeeM_ has finished, look at the file dbms-dataSize.log in the directory _${workingDir}_: there you will see the list of files to be downloaded along with their sizes.

Note: frequently the database files to be downloaded are compressed (.gz extension). To get the real size of the database, use a factor of 5 at minimum.

## Processing a new database

In the current version, _BeeDeeM_ can only process sequence databases in the following formats:

* Genbank and Genpept flat-files
* EMBL and Uniprot flat-files
* FASTA
* and some special formats such as CDD, BOLD and Eggnog

If you want to process a database complying with one of these formats, you can let _BeeDeeM_ do the work.

To process a specific database with _BeeDeeM_, you just have to create a database descriptor and place it in the directory ${installDir}/conf/descriptors. To create a new descriptor, refer to existing descriptors.

Note: is a new bank descriptor is not located in the standard `${installDir}/conf/descriptors` directory, then simply invoke BeeDeeM as follows to install that bank:

`bdm install -desc /absolute/path/to/bank-descriptor.dsc`

## Special case for flat-file sequence databases

Among others, SwissProt, TrEMBL and Genbank sequence databases exist in two formats: FASTA and flat-file.

The FASTA only contains the sequences and is used for preparing BLAST databases.

The flat-file format contains the sequences and the supplementary data (annotations, some biological classifications, _etc_.). It is by far the largest, but it includes essential information that the users will wish to consult. Consulting this information, for each sequence, can only be made efficient by a flat-file database indexing procedure. _BeeDeeM_ has such an indexing system as standard.

Thus, if you want to install and index databases complying with the Genbank or EMBL flat-file formats, you must not only download them but you must also index them. These operations are very easy to indicate in the database descriptors. Refer to the descriptors Uniprot\_TrEMBL.dsc and Genbank\_CoreNucleotide.dsc (directory ${installDir}/conf/descriptors) for examples of such processing. The file Uniprot\_TrEMBL.dsc describes the processing (downloading and indexing) of a database in EMBL format. The file Genbank\_CoreNucleotide.dsc describes the same processing but for a file in Genbank format.
