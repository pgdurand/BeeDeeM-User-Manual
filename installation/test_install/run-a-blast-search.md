# Run a BLAST search

_Note:_ we suppose that NCBI BLAST+ software is installed on you computer.

_BeeDeeM_ creates a BLAST databank for every sequence databank installed.

So, you can easily run BLAST jobs, as illustrated by this command-line snippet:

```
# We get a query sequence from BeeDeeM repository
$ query.sh -d protein -i 1433S_HUMAN -f fas > 1433S_HUMAN.fas

# We "BLASTp" that query against the installed Human subdivision of Uniprot_Swissprot
$ blastp -db /biobase/p/SwissProt_human/current/SwissProt_human/SwissProt_humanM \
         -query 1433S_HUMAN.fas -outfmt 5 -out 1433S_HUMAN.blastp
```

In turn, the BLAST result file (1433S\_HUMAN.blastp) can be viewed using the [BLAST Viewer software](https://github.com/pgdurand/BlastViewer).

[Read more](../../run-blast.md) about using BLAST with BeeDeeM-managed banks.
