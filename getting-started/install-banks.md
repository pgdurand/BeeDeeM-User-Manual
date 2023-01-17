# Install databanks

## Starting an installation process

### Using a global descriptor

This is the legacy way of using BeeDeeM to install a bank. The processing must be started by a user so that _BeeDeeM_ can access its various directories in read/write mode, particularly _${installDir}, ${workingDir}_ and _${biobaseDir}_.

After opening a session (via a terminal), proceed as follows:

```
bdm install <DESC>

    where
      - <DESC> is a global descriptor file name without its '.gd' extension.
        Such a file must be located in ${descriptors} directory.
```

Here is an example:

```
bdm install test
```

And there you go! This command starts a _BeeDeeM_ bank installation process using file '_test.gd_' located in _${descriptors}_.

Refer to the section [Control of execution](install-banks.md#control-of-execution) for more information about _BeeDeeM_ operation.

### Using a classic bank descriptor

Instead of using a global descriptor, it is possible to start BeeDeeM bank installation in a more direct way: all parameters usually provided using a global descriptor (a file) can be passed in directly to a command-line.

Get help by entering this command:

```
bdm install -h
```

A simple command-line would be:

```
bdm install -desc Uniprot_SwissProt -task download 

    where you can see all mandatory arguments:
      -desc Uniprot_SwissProt is a bank descriptor file name without its '.dsc' 
        extension.
        Such a file must be located in ${installDir}/conf/descriptors. Comma
        separated list of descriptors is accepted, e.g. Uniprot_SwissProt,PDB_protein.
      -task download instructs BeeDeeM to download and install Uniprot_SwissProt
      
```

You can control `bdm install` tool with some environment variables as stated [in this section](beedeem-configuration.md).&#x20;

## Starting a deferred process

Starting _BeeDeeM_ interactively is only possible if you are processing a small database. In most cases, it is recommended to start the processing using a job scheduler, such as SGE, SLURM or PBS.

BeeDeeM is designed to be used on computing clusters quite easily using a script such as:

```
#!/usr/bin/env bash
#PBS -q web
#PBS -l mem=4gb
#PBS -l ncpus=8
#PBS -l walltime=72:00:00

# Release of BeeDeeM to use
BDM_HOME="$SOFT/bioinfo/beedeem"
BDM_VER="5.0.0"

# Load BeeDeeM environment
module load java/1.8.0_121

# prefix of '.dsc' file that must exist in $BDM_HOME/conf/descriptor
DESCRIPTOR="Genbank_CoreNucleotide"
export KL_LOG_TYPE=console
$BDM_HOME/$BDM_VER/bdm install \
   -desc ${DESCRIPTOR} \
   >& "$HOME/beedeem/logs/${DESCRIPTOR}-pbs.out"
```

## Control of execution

You can monitor the progress of _BeeDeeM_ by consulting the file **dbms-XXX.log** located in the directory _${workingDir}_, where XXX identifies the descriptor used to start the process.

This log file is filled in during _BeeDeeM_ processing. The directory _${workingDir}_ might therefore contain a file kdms-XXX.log (file currently being used), and also the files kdms-XXX.logYYYYMMDD (log file dating from YYYYMMDD; YYYY is the year, MM is the month and DD is the day). When analysing _BeeDeeM_ logs, you must therefore analyse all of the dbms.log files corresponding to a given process.

```
Example: you start a process on 25/02/2017 which ends on 27/02/2017.
Then, you analyse the files:
    dbms-XXX.log, dbms-XXX.log20170226 and dbms-XXX.log20170225.
```

The examination of _BeeDeeM_ logs starts with reading the last (_i.e._ the most recent) log file (in our example, this is dbms-XXX.log).

If the processing was successful, you will see the following line at the end of the log file:

```
INFO | Processing ok.
```

This message indicates that the sequence databases were successfully installed on your system and your users now have access to the new versions of these banks. For more details, refer to the section [What to do after processing](banks-organization.md#what-to-do-after-processing).

If the processing failed, the following line will appear at the end of the log:

```
ERROR | Processing failed. Check WARN messages.
```

So, you can easily use grep command to check BeeDeeM logs as follows:

`grep "ERROR\|WARN" dbms-XXX.log`

`grep "PROCESSING: " dbms-XXX.log`

In case of errors/warnings, no sequence banks have been installed in production and your users will continue to use the database versions currently in production. For more details, refer to the section [What to do after processing](banks-organization.md#what-to-do-after-processing).
