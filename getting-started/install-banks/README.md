# Install databanks

## Starting a process interactively

### Using a global descriptor

This is the original way of using BeeDeeM to install a bank. The processing must be started by a user so that _BeeDeeM_ can access its various directories in read/write mode, particularly _${installDir}, ${workingDir}_ and _${biobaseDir}_.

After opening a session \(via a terminal\), proceed as follows:

```text
$ cd ${installDir}
$ ./install.sh <DESC>

    where
      - ${installDir}: replace by the directory where BeeDeeM is
        installed on your system.
      - <DESC> is a global descriptor file name without its '.gd' extension.
        Such a file must be located in ${confDir} of your BeeDeeM installation.
```

Here is an example:

```text
$ cd ${installDir}
$ ./install.sh test
```

And there you go! This command starts a _BeeDeeM_ bank installation process using file '_test.gd_' located in _${confDir}_.

Refer to the section [Control of execution](./#control-of-execution) for more information about _BeeDeeM_ operation.

### Using a single command-line

Instead of using a global descriptor, it is possible to start BeeDeeM bank installation in a more direct way: all parameters usually provided using a global descriptor \(a file\) can be passed in directly to a command-line.

Get help by entering this command:

```text
$ cd ${installDir}
$ ./install.sh -h
```

A simple command-line would be:

```text
$ ./install.sh -h -desc swissprot -task download 

    where you can see all mandatory arguments:
      -desc swissprot is a bank descriptor file name without its '.dsc' extension.
        Such a file must be located in ${installDir}/conf/descriptors. Comma
        separated list of descriptors is accepted, e.g. swissprot,PDB_protein.
      -task download instructs BeeDeeM to download and install swissprot
      
```

In addition to command-line arguments, it is possible to change default settings of BeeDeeM using environment variables, as follows: 

| Variable name | Value | Use |
| :--- | :--- | :--- |
| KL\_DEBUG | true, false | Set on/off DEBUG mode of BeeDeeM. Default is false. |
| KL\_WORKING\_DIR | An absolute path | If not set, log and working directories are set to java.io.tmp |
| KL\_CONF\_DIR | An absolute path | Absolute path to a home-made "conf" directory. If not set, use ${installDir}/conf |
| KL\_LOG\_TYPE | none, console, file | Set logging system. Choose between 'none' \(silent mode of BeeDeeM\), 'console' or 'file' \(default\). |
| KL\_LOG\_FILE | File name | When using KL\_LOG\_TYPE=file, set the file name. |

How to set such an environment variable? For instance, if you want to set KL\_LOG\_TYPE to none, do this on a bash shell \(Linux\):

```text
export KL_LOG_TYPE=none
./install.sh .../...
```

Finally, it is possible to override settings from "${installDir}/conf/dbms.config" configuration file directly using "java -D arguments" or by setting a standard environment variable. For that purpose, prefix "dbmf.config" property key with "KL\_"_._ For instance, if you want to override default "mirror.path" value, use either:

*  `java ... -DKL_mirror.path="/a/path"` in the Java command starting BeeDeeM bank installation;
* `export KL_mirror.path="/a/path"` on a Linux bash shell before calling BeeDeeM bank installation tool \(install.sh\).

## Starting a deferred process

Starting _BeeDeeM_ interactively is only possible if you are processing a small database. In most cases, it is recommended to start the processing at night or, even better, on a weekend.

Indeed, the installation of large banks such as the UniProt and Genbank databases is a long process as it requires the downloading and indexing of several 10’s of GB of data. The UniProt download is from FTP servers installed in Switzerland and Great Britain, and the Genbank database is retrieved from FTP servers installed in the USA. Therefore, it is better to start _BeeDeeM_ not in interactive mode but via the task scheduler of your operating system.

For large databanks, the idea is to start _BeeDeeM_ at night \(_e.g._ Central European time\) or during the weekend.

Deferred process is performed by using the system at/batch/cron under Linux/MacOSX or the Windows Task Manager.

This is how to start _BeeDeeM_ to install databanks listed in descriptor "default.gd" on February 26th, 2017 on a Unix system:

```text
$ at 0100 022617
at> ${installDir}/CmdLineInstall.sh default
at> [press CTRL+D]

where ${installDir} should be replaced with the directory KDMS is installed in.
```

Certainly, change the processing start date to suit your calendar!

## Control of execution

You can monitor the progress of _BeeDeeM_ by consulting the file **dbms-XXX.log** located in the directory _${workingDir}_, where XXX identifies the global descriptor used to start the process; considering the above example, we would have a look at file "dbms-default.log".

This log file is backed up during _BeeDeeM_ processing. The directory _${workingDir}_ might therefore contain a file kdms-XXX.log \(file currently being used\), and also the files kdms-XXX.logYYYYMMDD \(log file dating from YYYYMMDD; YYYY is the year, MM is the month and DD is the day\). When analysing _BeeDeeM_ logs, you must therefore analyse all of the dbms.log files corresponding to a given process.

```text
Example: you start a process on 25/02/2017 which ends on 27/02/2017.
Then, you analyse the files:
    dbms-XXX.log, dbms-XXX.log20170226 and dbms-XXX.log20170225.
```

The examination of _BeeDeeM_ logs starts with reading the last \(_i.e._ the most recent\) log file \(in our example, this is dbms-XXX.log\).

If the processing was successful, you will see the following line at the end of the log file:

```text
INFO | Processing ok.
```

This message indicates that the sequence databases were successfully installed on your system and your users now have access to the new versions of these banks. For more details, refer to the section [What to do after processing](../banks-organization.md#what-to-do-after-processing).

If the processing failed, the following line will appear at the end of the log:

```text
WARN | Processing failed. Check WARN messages.
```

In this case, no sequence databases have been installed in production and your users will continue to use the database versions currently in production. For more details, refer to the section [What to do after processing](../banks-organization.md#what-to-do-after-processing).

## BeeDeeM is running?

It is possible, at any time, to determine whether _BeeDeeM_ is running using Unix command 'ps':

```text
$ ps -ef | grep CmdLineInstaller
```

Use the Task Manager on Windows systems.

