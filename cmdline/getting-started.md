# Getting started

## Command to use

The command to start *BeeDeeM* is:

```
$ install.sh <descriptor>   [Linux, MacOSX]
c:\> install.bat <descriptor>  [Windows]
```

*Note:* during script execution, there is nothing displayed on the terminal whether something goes OK or wrong. However, *BeeDeeM* logs all its work in a dedicated log file located in ${workingDir}. Refer to [Directory structure](/directory_structure.md) for more information.


## *BeeDeeM* installation directory

We suppose we work on a Unix-base system in the rest of the manual. Windows users can easily adapt to their OS.

The *BeeDeeM* directory _${installDir}_ is organised as follows \(Linux/OSX defaults\):

| Directory | Contents | Default value |
| :--- | :--- | :--- |
| _${installDir}_ | Home directory of *BeeDeeM* | /opt/beedeem |
| _${installDir}/bin_ | Java libraries for *BeeDeeM* and its dependencies | /opt/beedeem/bin |
| _${installDir}/external_ | Native binaries \(such as makeblastdb\) for Linux, MacOSX or Windows | /opt/beedeem/external |
| _${installDir}/conf_ | *BeeDeeM* configuration files and databank descriptors | /opt/beedeem/conf |

## *BeeDeeM* databanks repository

*BeeDeeM* stores all the databanks under its supervision within a dedicated directory: _${biobaseRootDir}_. This directory is defined during the installation of *BeeDeeM*. Please refer to [Directory structure](/directory_structure.md).

## Configuration directory used during databank installation

*BeeDeeM* relies on a dedicated directory containing particular files called: **databank descriptor files**. These files instruct the software how to install databanks and they are located in _${installDir}/conf_, as stated above.

This configuration directory will be called _${conf}_ in the following sections.

