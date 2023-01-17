# Query databank repository

_BeeDeeM_ comes with an additional tool aims at querying databanks repository by entity ID. Such an ID can be either a sequence ID or an ontology ID.

That tool is only available from the command line.

_Note:_ during script execution, there is nothing displayed on the terminal whether something goes OK or wrong. However, _BeeDeeM_ logs all its work in a dedicated log file located in ${workingDir}. Refer to [Directory structure](../installation/directory\_structure.md) for more information.

## Command-line use

Command line takes three arguments, in this order:

```
bdm query -d <database> -i <seq_id> -f <format> -o <output>
```

and the result is directly dumped in standard output.

* **database** \[_required_]: type of repository to query. One of: n, p, d. When using d, use one of: d:taxon, d:EC, d:GO, d:CDD or d:InterPro. When using d:taxon, entry ID can be either a TaxID or a Taxonomy Name (e.g. organism, phylum, etc.). In latter case, Query Tool will dump Taxonomy path;
* **seq\_id** \[_required_]: either a single entry ID, a comma separated list of entry IDs of a path to a file of entry IDs. When using a file of IDs, provide a single ID per line;
* **format** \[_required_]: output format. One of: txt, fas, html, insd, finsd. When using dico repository type, txt format only applies.
* **output** \[optional]: output file to save results of query. Optional, default is stdout.

[Sample use case](../installation/test\_install/query-the-bank-repository.md).
