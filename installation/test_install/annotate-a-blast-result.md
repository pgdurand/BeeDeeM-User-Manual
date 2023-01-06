# Annotate a BLAST result

Let us terminate this mini-tutorial with another feature of BeeDeeM: its capability of introducing Features Table data into BLAST result files.

**How this feature is possible?**&#x20;

Only if the target databank contains features. A simple FASTA file does not contain such information. However, banks from Uniprot or Genbank do contain such information.

Ok, try this on the command-line:

```
bdm query -d protein -i 1433S_HUMAN -f txt
```

Among the many types of information, that Swissprot entry contains:

```
OX   NCBI_TaxID=9606;
.../...
DR   GO; GO:0005913; C:cell-cell adherens junction; IDA:BHF-UCL.
DR   GO; GO:0005737; C:cytoplasm; IDA:HPA.
DR   GO; GO:0030659; C:cytoplasmic vesicle membrane; TAS:Reactome.
.../...
DR   InterPro; IPR000308; 14-3-3.
DR   InterPro; IPR023409; 14-3-3_CS.
DR   InterPro; IPR023410; 14-3-3_domain.
.../...
FT   CHAIN         1    248       14-3-3 protein sigma.
FT                                /FTId=PRO_0000058643.
FT   SITE         56     56       Interaction with phosphoserine on
FT                                interacting protein.
```

These are: taxonomy ID (OX line), GeneOntology and InterPro ontology IDs (DR lines) and a Features Table (FT lines).

**Let's annotate a BLAST result!**

Now, you can annotate a BLAST result as follows (we resume the above example where we produce the BLAST file: 1433S\_HUMAN.blastp):

```
bdm annot -i 1433S_HUMAN.blastp -o 1433S_HUMAN.zml -type full -writer zml
```

_Note_: during script execution, there is nothing displayed on the terminal whether something goes wrong. However, _BeeDeeM_ logs all its work in a dedicated log file located in _${workingDir}_.

A 'zml' file is a dedicated zip-compressed XML format capable of representing what we call a [Rich Search Result](https://github.com/pgdurand/Bioinformatics-Core-API/tree/master/src/bzh/plealog/bioinfo/api/data/searchresult), i.e. a BLAST data model augmented with Features (standard NCBI BLAST XML format is not capable of doing that).

You can analyze the content of '1433S\_HUMAN.zml' using the [BLAST Viewer software](https://github.com/pgdurand/BlastViewer) or by writing your own home-made tool using the [Bioinformatics Core API](https://github.com/pgdurand/Bioinformatics-Core-API).

[Read more](../../utils/cmdline-annotate.md) about annotating BLAST results with BeeDeeM-managed banks.
