# Query databank repository

_BeeDeeM_ comes with an additional tool aims at querying databanks repository by entity ID. Such an ID can be either a sequence ID or an ontology ID.

That tool is only available from the command line and is called:

* query.sh: to be used on Linux or Mac OSX system
* query.bat: to be used on Windows system

_Note:_ during script execution, there is nothing displayed on the terminal whether something goes OK or wrong. However, _BeeDeeM_ logs all its work in a dedicated log file located in ${workingDir}. Refer to [Directory structure](../installation/directory_structure.md) for more information.

## Command-line use

Command line takes three arguments, in this order:

```text
query.sh -d <database> -i <seq_id> -f <format>
```

and the result is directly dumped in standard output.

* **database** \[_required_\]: use either "dico", "nucleotide" or "protein";
* **seq\_id** \[_required_\]: an entity ID;
* **format** \[_required_\]: use either "txt" \(default\), "html", "insd", "fas" or "finsd".

[Sample use case](../installation/test_install/#query-the-beedeem-bank-repository).

In addition, some parameters can be passed to the JVM for special configuration purposes:

* -DKL\_DEBUG=true ; if true, log will be in debug mode
* -DKL\_WORKING\_DIR=an\_absolute\_path ; if not set, log and working directories are set to java.io.tmp
* -DKL\_LOG\_FILE=a\_file\_name ; if set, creates a log file with that name within KL\_WORKING\_DIR

