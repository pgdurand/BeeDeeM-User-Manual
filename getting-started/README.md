# Use BeeDeeM from the command-line

## Command to use

The command to start _BeeDeeM_ is:

```text
$ install.sh <descriptor>   [Linux, MacOSX]
c:\> install.bat <descriptor>  [Windows]
```

_Note:_ during script execution, there is nothing displayed on the terminal whether something goes OK or wrong. However, _BeeDeeM_ logs all its work in a dedicated log file located in ${workingDir}. Refer to [Directory structure](../installation/directory_structure.md) for more information.

## _BeeDeeM_ installation directory

We suppose we work on a Unix-base system in the rest of the manual. Windows users can easily adapt to their OS.

The _BeeDeeM_ directory _${installDir}_ is organised as follows \(Linux/OSX defaults\):

| Directory | Contents | Default value |
| :--- | :--- | :--- |
| _${installDir}_ | Home directory of _BeeDeeM_ | /opt/beedeem |
| _${installDir}/bin_ | Java libraries for _BeeDeeM_ and its dependencies | /opt/beedeem/bin |
| _${installDir}/external_ | Native binaries \(such as makeblastdb\) for Linux, MacOSX or Windows | /opt/beedeem/external |
| _${installDir}/conf_ | _BeeDeeM_ configuration files and databank descriptors | /opt/beedeem/conf |

## _BeeDeeM_ databanks repository

_BeeDeeM_ stores all the databanks under its supervision within a dedicated directory: _${biobaseRootDir}_. This directory is defined during the installation of _BeeDeeM_. Please refer to [Directory structure](../installation/directory_structure.md).

## Configuration directory used during databank installation

_BeeDeeM_ relies on a dedicated directory containing particular files called: **databank descriptor files**. These files instruct the software how to install databanks and they are located in _${installDir}/conf_, as stated above.

This configuration directory will be called _${conf}_ in the following sections.

