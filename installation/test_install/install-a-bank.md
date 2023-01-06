# Install a bank

You can run a bank installation from the command-line as follows:

```
bdm install -desc SwissProt_human

where - 'SwissProt_human' is the name of the bank descriptor to use to start
        bank installation (more on this later)
```

_Note_: during script execution, there is nothing displayed on the terminal whether something goes 'ok' or 'wrong'. However, _BeeDeeM_ logs all its work in a dedicated log file located in _${workingDir}_

Once execution finishes, check the contents of the _BeeDeeM_ log file.

```
$ cat ${workingDir}/dbms-SwissProt_human.log | grep WARN

where ${workingDir} should be replaced by the working directory of BeeDeeM
```

If there are some WARN lines in the logs, then refer to the section [Appendix – Common errors](../../getting-started/common-errors.md).

Otherwise, it means the SwissProt\_human bank (Uniprot annotated formatand BLAST formated bank) is now installed on your system.

### Common descriptors

BeeDeeM is provided with a common list of bank descriptors available in its [conf/descriptors ](https://github.com/pgdurand/BeeDeeM/tree/master/conf/descriptors)folder. These are the files suffixed with '.dsc' extension. Simply provide that file name (without path and extension) to the install.sh command line tool.

In our above example:

`install.sh -desc` SwissProt\_human

implies that you have the file 'SwissProt\_human.dsc' within 'conf/descriptors' folder of BeeDeeM.

You can get an overview all all available bank descriptors using:

`bdm desc -l`

Bank descriptors are fully described in a separate [section](../../getting-started/using-descriptors.md).&#x20;

### Install more databanks

If the above test was successful, you can continue to install other databanks:

* from the command-line, jump to [CmdLineInstaller](../../getting-started/)
* from the graphical interface, jump to [UiInstaller](../../getting-started-1/)
