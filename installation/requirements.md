# Requirements

_BeeDeeM_ is a mostly a Java software, so it is available for _Linux_, _MacOS X and Windows_ operating systems.&#x20;

However, if you plan to use BeeDeeM on cluster infrastructures and benefit from the capability of the BeeDeeM extended task engine to submit jobs on computing nodes, then you can only rely on a Linux OS.

## Software

_BeeDeeM_ uses the following software dependencies:

* for installation and use: an [_Oracle Java Runtime Environment_ (JRE)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html), version 1.8 or higher
* for use on Linux and macOS: bash version 4 or higher and coreutils (to benefit from the realpath command)

If you plan to install BeeDeeM using legacy procedure, the following software must be installed before installing _BeeDeeM_: _JRE 1.8+_.

For other types of installation: either Docker, Singularity or Anaconda has to be installed on your host system.

## Hardware

Being a bioinformatics databanks manager software, _BeeDeeM_ mostly requires a potentialy huge amont of disk storage; of course, it fully depends on your needs. Generally, the disk space required must be at least twice the size of the databases to be generated. In effect, when _BeeDeeM_ installs a new version of a database, its already installed copy remains available to the users.

## Ressources

BeeDeeM requires at least 4 CPUs, 4 Gb RAM and from half an hour (PDB) up to 48 hours (TrEMBL) to install a databank. Running time depends on network speed, too.

Now, if your bank descriptors (the configuration files telling BeeDeeM how to install banks; see [#what-is-a-databank-descriptor](../getting-started/using-descriptors.md#what-is-a-databank-descriptor "mention")) use external scripts to achieve additional post-processings, higher ressources may be required. As an example, installing TrEMBL with BLAST V4 and V5 bank formats, Diamond and Bowtie2 indexes require up to 32 Go RAM (using 4 CPUs).

