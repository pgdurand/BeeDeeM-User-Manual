# Run BLAST search

_BeeDeeM_ automatically converts all sequence databanks to a BLAST databank.

## BLAST bank format

_BeeDeeM_ uses NCBI's _makeblastdb_ tool to prepare BLAST databanks, so they can be directly used with the BLAST suite of softwares; either _legacy BLAST_ (_blastall_ program) or _BLAST+_.

## Command-line use of BLAST

We suppose BLAST is already installed on your system.

Let us suppose you have installed the PDB databank using _BeeDeeM_. Following the [Databanks organization](getting-started/banks-organization.md), it is installed in directory:

```
${biobaseRootDir}/p/PDB_proteins/current/PDB_proteins
```

Say, you have a query file containing some protein sequences: p12265.fas

Now, to run a BLAST search, simply use this command:

```
blastp \
      -db ${biobaseRootDir}/p/PDB_proteins/current/PDB_proteins/PDB_proteinsM \
      -query p12265.fas \
      -outfmt 5 \
      -out result.xml
```

Of course, adapt the command-line to your needs.

The important point here, is the name of the BLAST bank. In the directory where PDB is installed, we locate the file ending with **M.pal**: this is the BLAST bank alias file name to provide to BLAST.

In you have a nucleotide bank installed, look for file ending with **M.nal** instead.

[Sample use case](installation/test\_install/#run-a-blast-search).

## View BLAST results

BLAST results prepared using '-outfmt 5' argument (see command-line, above) are XML files that can be viewed with [BLAST Viewer](https://github.com/pgdurand/BlastViewer).

## Quickly locate BLAST banks

You can use [info](utils/list-banks.md) tool to get the list of BLAST banks. [Read more](utils/list-banks.md).
