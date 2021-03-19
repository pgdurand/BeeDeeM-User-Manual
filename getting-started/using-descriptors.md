# Databank descriptors

## What is a databank descriptor ?

A databank descriptor is a text file containing the instructions used by _BeeDeeM_ to download and install databanks.

There are two types of descriptor:

* **bank descriptor** \(.dsc file\): descriptor used to describe the installation of a single databank
* **global descriptor** \(.gd file\): descriptor used to start the installation of one or several databanks

## Description of databases to be managed: the bank descriptor

By default, _BeeDeeM_ provides a non-exhaustive list of **descriptors** for processing various sequence databanks and biological classifications \(ontologies\). All of these files are suffixed with extension “.dsc” and are located in _${conf}_ directory.

Each file contains a group of instructions used by _BeeDeeM_:

* to download \(via FTP\) all files making up the complete distribution of a database 
* to process the downloaded files to make them usable \(decompressing, un-archiving, indexing, etc.\)

Here is a sample bank descriptor aims at installing Uniprot\_SwissProt:

```text
# Bank name
db.name=Uniprot_SwissProt
# Bank description
db.desc=UniprotKB/SwissProt databank (contains annotations).
# Bank type
db.type=p
# Bank location
db.ldir=${mirrordir}|p|Uniprot_SwissProt

# Server access
ftp.server=ftp.expasy.org
ftp.port=21
ftp.uname=anonymous
ftp.pswd=user@company.com
# Directory to locate files to download
ftp.rdir=/databases/uniprot/current_release/knowledgebase/complete
ftp.rdir.exclude=

# File(s) to retrieve
db.files.include=uniprot_sprot.dat.gz
db.files.exclude=

# Processing tasks
tasks.unit.post=gunzip,idxsw
tasks.global.post=delgz,deltmpidx,formatdb(lclid=false;check=true;nr=true)

# Keep previous release or not
history=0
```

The use of such a file will be explained in the next section.

The full format of the database descriptors is documented in section [Databank descriptor format](descriptors-format.md).

## Description of processing to be performed: the global descriptor

The processing that _BeeDeeM_ will perform is described in a **global descriptor**.

Here is an example of such a descriptor:

```text
# List of banks to retrieve (use bank descriptor name)
db.list=PDB_protein

# What to do (download or info)
db.main.task=download

# Restart a failed process
resume.date=none

# Parameters of the loader engine
task.delay=1000
ftp.delay=5000
ftp.retry=3

# Do we have to send an email to DBMS manager?
mail.smtp.host=
mail.smtp.port=
mail.smtp.sender.mail=
mail.smtp.sender.pswd=
mail.smtp.recipient.mail=
```

By default, _BeeDeeM_ has a “test” descriptor for processing the installation of PDB Protein.

This descriptor is the file named 'test.gd' located in the directory _${conf}_.

Note: We will use this file 'test.gd' in the rest of this manual to explain how to use _BeeDeeM_. However, you can create other descriptors \(_e.g._ by deriving them from 'test.gd'\), but always be sure to save them in the directory _${conf}_.

Before starting any processing, it is **VERY IMPORTANT** to check the following two lines in the global descriptor:

```text
db.list=PDB_Protein
resume.date=none
```

The first line is a comma separated list of database descriptors to use \(without their ".dsc" extension\). It defines which databank\(s\) will be installed during a single _BeeDeeM_ processing.

The second line gives a restart date. This line is only used in the case of a restart after a failure. If you start _BeeDeeM_ for the first time or if you are updating the databases, it is absolutely imperative to set "resume.date" to the value _none_. All of this is explained in section [Advanced uses](advanced-uses/).

**But now, let's see how to install a databank using these descriptors!**

