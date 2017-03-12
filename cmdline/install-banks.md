# Install databanks

## Starting a process interactively

The processing must be started by a user so that *BeeDeeM* can access its various directories in read/write mode, particularly _${installDir}, ${workingDir}_ and _${biobaseDir}_.

After opening a session \(via a terminal\), proceed as follows:

```
$ cd ${installDir}
$ ./CmdLineInstall.sh <DESC>

    where 
      - ${installDir} is replaced by the directory where BeeDeeM is 
        installed in on your system, and test is the name of the global 
        descriptor (without its extension .gd) to be used. 
      - <DESC> is a global descriptor file name without its '.gd' extension
```

Here is an example:

```
$ cd ${installDir}
$ ./CmdLineInstall.sh test
```

And there you go! This command starts a *BeeDeeM* bank installation process using file '*test.gd*' located in *${confDir}*.

Refer to the section [Control of execution](#control-of-execution) for more information about *BeeDeeM* operation.

## Starting a deferred process

Starting *BeeDeeM* interactively is only possible if you are processing a small database. In most cases, it is recommended to start the processing at night or, even better, on a weekend.

Indeed, the installation of large banks such as the UniProt and Genbank databases is a long process as it requires the downloading and indexing of several 10’s of GB of data. The UniProt download is from FTP servers installed in Switzerland and Great Britain, and the Genbank database is retrieved from FTP servers installed in the USA. Therefore, it is better to start *BeeDeeM* not in interactive mode but via the task scheduler of your operating system.

For large databanks, the idea is to start *BeeDeeM* at night \(_e.g._ Central European time\) or during the weekend.

Deferred process is performed by using the system at/batch/cron under Linux/MacOSX or the Windows Task Manager.

This is how to start *BeeDeeM* to install databanks listed in descriptor "default.gd" on February 26th, 2017 on a Unix system:

```
$ at 0100 022617
at> ${installDir}/CmdLineInstall.sh default
at> [press CTRL+D]

where ${installDir} should be replaced with the directory KDMS is installed in.
```

Certainly, change the processing start date to suit your calendar!

## Control of execution

You can monitor the progress of *BeeDeeM* by consulting the file **dbms-XXX.log** located in the directory _${workingDir}_, where XXX identifies the global descriptor used to start the process; considering the above example, we would have a look at file "dbms-default.log".

This log file is backed up during *BeeDeeM* processing. The directory _${workingDir}_ might therefore contain a file kdms-XXX.log \(file currently being used\), and also the files kdms-XXX.logYYYYMMDD \(log file dating from YYYYMMDD; YYYY is the year, MM is the month and DD is the day\). When analysing *BeeDeeM* logs, you must therefore analyse all of the dbms.log files corresponding to a given process.

```
Example: you start a process on 25/02/2017 which ends on 27/02/2017. 
Then, you analyse the files:
    dbms-XXX.log, dbms-XXX.log20170226 and dbms-XXX.log20170225.
```

The examination of *BeeDeeM* logs starts with reading the last (*i.e.* the most recent) log file \(in our example, this is dbms-XXX.log\).

If the processing was successful, you will see the following line at the end of the log file:

```
INFO | Processing ok.
```

This message indicates that the sequence databases were successfully installed on your system and your users now have access to the new versions of these banks. For more details, refer to the section [What to do after processing](/cmdline/banks-organization.md#what-to-do-after-processing).

If the processing failed, the following line will appear at the end of the log:

```
WARN | Processing failed. Check WARN messages.
```

In this case, no sequence databases have been installed in production and your users will continue to use the database versions currently in production. For more details, refer to the section [What to do after processing](/cmdline/banks-organization.md#what-to-do-after-processing).

## BeeDeeM is running?

It is possible, at any time, to determine whether _BeeDeeM_ is running using Unix command 'ps':

```
$ ps -ef | grep CmdLineInstaller
```
Use the Task Manager on Windows systems.