# Descriptors format

## Using FTP servers

As stated earlier, a databank is installed by _BeeDeeM_ by using a configuration file called a databank descriptor. There is a descriptor file for each databank to install, and each descriptor follows a similar file format.

Here is an example of the descriptor used to install the PDB protein databank from the NCBI FTP server:

```text
db.name=PDB_proteins                                       (1)
db.desc=PDB Protein databank (Klast/Blast only).           (2)
db.type=p                                                  (3)
db.ldir=${mirrordir}|p|PDB_proteins                        (4)

ftp.rdir=/blast/db/FASTA/                                  (5)
ftp.rdir.exclude=                                          (6)

db.files.include=pdbaa.gz                                  (7)
db.files.exclude=                                          (8)

tasks.unit.post=gunzip,idxfas                              (9)
tasks.global.post=formatdb(lclid=false;check=true;nr=true) (10)

ftp.server=ftp.ncbi.nih.gov                                (11)
ftp.port=21                                                (12)
ftp.uname=anonymous                                        (13)
ftp.pswd=user@institute.org                                (14)

history=0                                                  (15)
```

**\(1\) / \(2\)** define databank name and description. Be aware that the databank name must match the descriptor file name; i.e. databank named “PDB\_proteins” must be saved within a file called “PDB\_proteins.dsc”

**\(3\)** defines the databank type. Accepted value is either “p” or “n”, which stands for “protein” or “nucleotide” databank, respectively.

**\(4\)** defines the directory where _BeeDeeM_ will deploy the databank. Format must start with the variable ${mirrordir}, followed by the databank type, either “p” or “n”, followed by the databank name; as you can see the databank name matches the value of “db.name”. Carefully use “\|” character between each part of the path.

**\(5\)/\(6\)** define the directories to include or exclude to locate files to retrieve from the FTP server. Accepted values are comma-separated list of directories; regular expressions are accepted.

**\(7\)/\(8\)** define the list of files to include or exclude. Accepted values are comma-separated list of files; regular expressions are accepted.

**\(9\)/\(10\)** define the tasks to apply to downloaded files; tasks are described [here](./#unit-tasks).

**\(11\)/\(14\)** define the access to the FTP server.

**\(15\)** defines whether or not _BeeDeeM_ should keep older releases of a databank; default value is 0, that means _BeeDeeM_ will delete the “old” release of a databank as soon as the latest release has been installed.

## Using local files

Instead of using FTP servers, you can also install databanks from personal sequences files. In such cases, you simply setup a “local” databank descriptor, as follows.

Given our previous example, remove lines \(7\)/\(8\) and \(11\) to \(14\) since you do not use FTP access. Then, add the following two lines:

```text
local.rdir=|path|to|my[files
local.rdir.exclude=
```

that simply define the directories to include or exclude to locate files on your local file system. Accepted values are comma-separated list of directories; regular expressions are accepted.

Carefully use “\|” character between each part of the path; i.e. do not use Unix path separator \(/\), nor the Windows one \(\).

## Unit tasks

One of the key feature of a databank descriptor \('.dsc' files located in ${conf} directory of _BeeDeeM_\) is to instruct the Databank Manager what to do with the downloaded data files; for example, sequence data files are available as compressed files \(e.g. '.dat.gz' files from the Uniprot databank\).

To be used by BLAST for instance, they have to be uncompressed, then converted to Fasta files and finally transformed to a Blast databank using the NCBI's 'formatdb/makeblastdb' utility.

This is the purpose of the two fields 'Unit tasks' and 'Global tasks' to let you specify what to do on each file \(unit task\) and on all files alltogether \(global task\). Taking the example of 'Refseq\_Viruses.dsc' databank descriptor, here are the two fields of interest:

```text
tasks.unit.post=gunzip,idxgb
tasks.global.post=delgz,deltmpidx,formatdb(lclid=false;check=true;nr=true)
```

Each of these two fields have to be filled in with available system tasks. The following tables give an overview of these tasks.

| Unit task name | arguments | Description |
| :--- | :--- | :--- |
| _gunzip_ | n/a | uncompress a gzip-compressed file |
| _untar_ | n/a | unarchive a Unix TAR file |
| _idxgb_ | taxinc,taxexc | create the sequence annotation index for a Genbank file \(1\) |
| _idxgp_ | taxinc,taxexc | create the sequence annotation index for a Genpept file \(1\) |
| _idxem_ | taxinc,taxexc | create the sequence annotation index for a EMBL file \(1\) |
| _idxsw_ | taxinc,taxexc | create the sequence annotation index for a Uniprot file \(1\) |
| _idxfas_ | n/a | create the sequence annotation index for a Fasta file |
| _idxdico_ | type,file | create the data index for a the biological classification file \(2\) |
| script | name,path | execute an external script \(3\).  |

_\(1\)_ Arguments 'taxinc' and 'taxexc' are optional and can be used to prepare taxonomic specific databanks. More on this in the section called “Preparing a taxonomic specific data subset”.

_\(2\)_ Argument 'type' is mandatory and specifies the biological classification type. Accepted value for this arguement is one of: tax \(NCBI Taxonomic Classification\), ipr \(Interpro term dictionary\), pfam \(Pfam term dictionary\), go \(Gene Ontology term dictionary\), ecc and ecd \(Enzyme Classification\). Argument 'file' is optional and specifies the file name to index.

\(3\) name and path arguments are mandatory. Default script location is 'conf/scripts'. An external script aims at executing any type of tasks that are not already available in standard BeeDeeM tasks. You can review an example of using an external task by looking at script sample 'hello\_world.sh' \(located in 'conf/scripts'\), along with 'PDB\_proteins\_task.dsc' file \(located in 'conf/descriptors'\). When providing scripts within standard loication \('conf/scripts'\), only provide script file name as value for argument 'path' of 'script' task. Otherwise, use full path.

## Global tasks

| Global task name | arguments | Description |
| :--- | :--- | :--- |
| _delgz_ | n/a | delete gzip files |
| _deltar_ | n/a | delete Unix TAR file |
| _deltmpidx_ | n/a | delete working directories and/or files created during an indexing task |
| _formatdb_ | lclid, check, nr, taxinc, taxexc, volsize, silva, taxonomy | invoke the NCBI's _formatdb/makeblastdb_ tool to create a BLAST databank from a set of FASTA sequence files \(4\) |
| script | name,path | execute an external script \(provide same feature as 'script' task on unit task\) |

\(4\) More on this in the section “Tuning BLAST databank maker”, below.

## Databank descriptor samples

To help you in learning how to use these tasks, the best way consists in starting from databank descriptors provided with _BeeDeeM_. Most of them can be used as templates to create new descriptors enabling the installation of specific data sets prepared from public source of data.

For example, if you want to see how to install \(1\) protein set of sequences available from the NCBI Genome Directory and \(2\) the Human subset of sequences from the UniprotKB/Swissprot, have a look at the following descriptors:

| Descriptor name | description |
| :--- | :--- |
| _Yersinia\_Angola\_prot_ | show how to install the Yersinia pestis Angola proteome from GenBank/Genomes Directory \(Blast bank only\) |
| _Yersinia\_all\_but\_Angola\_prot_ | show how to install all Yersinia pestis proteomes, excluding Angola, from GenBank/Genomes Directory \(Blast bank only\) |
| _Arabidopsis\_thaliana\_prot_ | show how to install the Arabidopsis thaliana proteome from GenBank/Genomes Directory \(Blast bank only\) |
| _SwissProt\_human_ | how to create a Human subset of UniprotKB/SwissProt: sequence annotations + Blast banks |
| PDB\_proteins\_task | how to call an external task; use of 'script' task |

## Tuning BLAST databank maker

_BeeDeeM_ can use either NCBI's "formatdb" \(legacy BLAST\) or "makeblastdb" \(BLAST+\) to convert FASTA files to a BLAST databank. Whatever the tool used, _BeeDeeM_'s task is called 'formatdb'?

In the table 'Global tasks', all arguments of global task 'formatdb' are optional.

Arguments 'lclid', 'check' and 'nr' only accept boolean values \(true or false\), 'taxinc' and 'taxexc' accept list of NCBI taxonomic IDs.

When arguments are omitted, default values are: lclid=false, check=true, nr=true and nothing is set by default for taxonomic constraints.

* argument 'lclid' specifies whether or not formatdb should use local sequence IDs \(see comment below\).
* argument 'check' specifies whether or not sequence files have to be checked for their content.
* argument 'nr' specifies whether or not sequence files have to checked for sequence ID redundancy.
* arguments 'taxinc' and 'taxexc' specify which sequences should be retained \(taxinc\) or discarded \(taxexc\) based on sequence taxonomic identifiers. More on this in the section called “Preparing a taxonomic specific data subset”.
* argument 'volsize' sets the size of a Fasta volume ; unit is Gb, and default value is 2 \(i.e. 2 Gb\) when 'volsize' is not set. Parameter 'volsize' can be used for large databank: if a source databank sizes 24 Gb, task 'formatdb' will create 12 Fasta volumes sizing 2 Gb each. If you use 'volsize=6', then 'formatdb' will create 4 Fasta volumes.
* argument 'silva' specifies whether or not the Fasta files contain taxonomy data formatted using Silva rules \(i.e. description is followed by plain text taxonomy classification data\).
* argument 'taxonomy' specifies whether or not the Fasta files contain taxonomy data formatted using NCBI rules \(i.e. description is followed by plain text taxon scientific name surrounded by square brackets\).

The NCBI's "formatdb/makeblastdb" tool expects to have Fasta files where the definition line contains sequence IDs that meet some particular criteria defined by the NCBI: a sequence ID is made of two parts, 'db\|id', where 'db' is a databank code and 'id' is a sequence ID \(e.g. sp\|P12267, gi\|1311386\|pdb\|1cbg\).

If your Fasta files do not respect that format, set argument 'lclid' to true, otherwise "formatdb/makeblastdb" will fail in converting the source files into a Blast databank.

## Global Descriptor format

A stated above, a databank descriptor describes how to install a single particular databank.

Now, we have to use a global descriptor to effectively install one or several databanks.

Let us take an example to understand the global descriptor format: "test.gd" located in the _${conf}_ directory.

```text
db.list=PDB_protein            (1)

db.main.task=download          (2)

resume.date=none               (3)

task.delay=1000                (4)
ftp.delay=5000                 (5)
ftp.retry=3                    (6)

mail.smtp.host=                (7)
mail.smtp.port=
mail.smtp.sender.mail=
mail.smtp.sender.pswd=
mail.smtp.recipient.mail=
```

**\(1\)** Comma separated list of databank descriptor files describing what to download/process. Do not put space characters in this list. All names listed here correspond to files having the extension '.dsc'.

**\(2\)** The main task to execute. Must be one of the two following keys: 'info' or 'download'. Use 'info' to just retrieve the list of files to download/process. Use 'download' to actually donwload/process files. When using 'info', the list of files \(along with their size\) is dumpped in the log file of the software.

**\(3\)** Resume a previously aborted process. To do that, replace 'none' by the process date using the format yyyymmdd \(ex: 20071027\). See [Restart after failure](../advanced-uses/#restart-after-failure) for more information.

**\(4\)** Delay \(ms\) between two consecutive task executions. Please follow recommendations of databank providers \(_e.g._ NCBI, EBI\).

**\(5\)** Delay \(ms\) between two consecutive FTP connections. Please follow recommendations of databank providers \(_e.g._ NCBI, EBI\).

**\(6\)** Maximum number of attempts to download a single file.

**\(7\)** Mailer configuration used to send an email to _BeeDeeM_ administrator when an installation fails. Leave values empty if no mailer available.

