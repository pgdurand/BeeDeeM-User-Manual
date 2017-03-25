# Databank Descriptor format

## Using FTP servers

As stated earlier, a databank is installed by *BeeDeeM* by using a configuration file called a databank descriptor. There is a descriptor file for each databank to install, and each descriptor follows a similar file format. 

Here is an example of the descriptor used to install the PDB protein databank from the NCBI FTP server: 


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
	
**(1) / (2)** define databank name and description. Be aware that the databank name must match the descriptor file name; i.e. databank named “PDB_proteins” must be saved within a file called “PDB_proteins.dsc”

**(3)** defines the databank type. Accepted value is either “p” or “n”, which stands for “protein” or “nucleotide” databank, respectively.

**(4)** defines the directory where *BeeDeeM* will deploy the databank. Format must start with the variable ${mirrordir}, followed by the databank type, either “p” or “n”, followed by the databank name; as you can see the databank name matches the value of “db.name”. Carefully use “|” character between each part of the path.

**(5)/(6)** define the directories to include or exclude to locate files to retrieve from the FTP server. Accepted values are comma-separated list of directories; regular expressions are accepted.

**(7)/(8)** define the list of files to include or exclude. Accepted values are comma-separated list of files; regular expressions are accepted.

**(9)/(10)** define the tasks to apply to downloaded files; tasks are described [here](/cmdline/descriptors-format.md#unit-tasks).

**(11)/(14)** define the access to the FTP server.

**(15)** defines whether or not *BeeDeeM* should keep older releases of a databank; default value is 0, that means *BeeDeeM* will delete the “old” release of a databank as soon as the latest release has been installed.

## Using local files

Instead of using FTP servers, you can also install databanks from personal sequences files. In such cases, you simply setup a “local” databank descriptor, as follows. 

Given our previous example, remove lines (7)/(8) and (11) to (14) since you do not use FTP access. Then, add the following two lines:

	local.rdir=|path|to|my[files
	local.rdir.exclude=

that simply define the directories to include or exclude to locate files on your local file system. Accepted values are comma-separated list of directories; regular expressions are accepted. 

Carefully use “|” character between each part of the path; i.e. do not use Unix path separator (/), nor the Windows one (\).

## Unit tasks

One of the key feature of a databank descriptor ('.dsc' files located in ${conf} directory of *BeeDeeM*) is to instruct the Databank Manager what to do with the downloaded data files; for example, sequence data files are available as compressed files (e.g. '.dat.gz' files from the Uniprot databank). 

To be used by BLAST for instance, they have to be uncompressed, then converted to Fasta files and finally transformed to a Blast databank using the NCBI's 'formatdb/makeblastdb' utility. 

This is the purpose of the two fields 'Unit tasks' and 'Global tasks' to let you specify what to do on each file (unit task) and on all files alltogether (global task). Taking the example of 'Refseq_Viruses.dsc' databank descriptor, here are the two fields of interest:

	tasks.unit.post=gunzip,idxgb
	tasks.global.post=delgz,deltmpidx,formatdb(lclid=false;check=true;nr=true)

Each of these two fields have to be filled in with available system tasks. The following tables give an overview of these tasks.

| Unit task name | arguments | Description |
| :--- | :--- | :--- |
| _gunzip_ | n/a | uncompress a gzip-compressed file |
| _untar_ | n/a | unarchive a Unix TAR file |
| _idxgb_ | taxinc,taxexc | create the sequence annotation index for a Genbank file (1) |
| _idxgp_ | taxinc,taxexc | create the sequence annotation index for a Genpept file (1) |
| _idxem_ | taxinc,taxexc | create the sequence annotation index for a EMBL file (1) |
| _idxsw_ | taxinc,taxexc | create the sequence annotation index for a Uniprot file (1) |
| _idxfas_ | n/a | create the sequence annotation index for a Fasta file |
| _idxdico_ | type,file | create the data index for a the biological classification file (2) |

*(1)* Arguments 'taxinc' and 'taxexc' are optional and can be used to prepare taxonomic specific databanks. More on this in the section called “Preparing a taxonomic specific data subset”.


## Global tasks

| Global task name | arguments | Description |
| :--- | :--- | :--- |
| _delgz_ | n/a | delete gzip files |
| _deltar_ | n/a | delete Unix TAR file |
| _deltmpidx_ | n/a | delete working directories and/or files created during an indexing task |
| _formatdb_ | lclid, check, nr, taxinc, taxexc, volsize, silva, taxonomy | invoke the NCBI's *formatdb/makeblastdb* tool to create a BLAST databank from a set of FASTA sequence files (3) |

(3) More on this in the section “Tuning BLAST databank maker”, below.

## Databank descriptor samples


For example, if you want to see how to install (1) protein set of sequences available from the NCBI Genome Directory and (2) the Human subset of sequences from the UniprotKB/Swissprot, have a look at the following descriptors:
| :--- | :--- |
| _Yersinia_Angola_prot_ | show how to install the Yersinia pestis Angola proteome from GenBank/Genomes Directory (Blast bank only) |
| _Yersinia_all_but_Angola_prot_ | show how to install all Yersinia pestis proteomes, excluding Angola, from GenBank/Genomes Directory (Blast bank only) |
| _Arabidopsis_thaliana_prot_ | show how to install the Arabidopsis thaliana proteome from GenBank/Genomes Directory (Blast bank only) |
| _SwissProt_human_ | how to create a Human subset of UniprotKB/SwissProt: sequence annotations + Blast banks |

## Tuning BLAST databank maker













## Global Descriptor format

A stated above, a databank descriptor describes how to install a single particular databank.

Now, we have to use a global descriptor to effectively install one or several databanks.

Let us take an example to understand the global descriptor format: "test.gd" located in the *${conf}* directory.

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

**(1)** Comma separated list of databank descriptor files describing what to download/process. Do not put space characters in this list. All names listed here correspond to files having the extension '.dsc'.

**(2)** The main task to execute. Must be one of the two following keys: 'info' or 'download'. Use 'info' to just retrieve the list of files to download/process. Use 'download' to actually donwload/process files. When using 'info', the list of files (along with their size) is dumpped in the log file of the software.

**(3)** Resume a previously aborted process. To do that, replace 'none' by the process date using the format yyyymmdd (ex: 20071027). See [Restart after failure](/cmdline/advanced-uses.md#restart-after-failure) for more information.

**(4)** Delay (ms) between two consecutive task executions. Please follow recommendations of databank providers (*e.g.* NCBI, EBI).

**(5)** Delay (ms) between two consecutive FTP connections. Please follow recommendations of databank providers (*e.g.* NCBI, EBI).

**(6)** Maximum number of attempts to download a single file.

**(7)** Mailer configuration used to send an email to *BeeDeeM* administrator when an installation fails. Leave values empty if no mailer available.