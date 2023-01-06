# Requirements

_BeeDeeM_ is mostly a Java software, so it is available for _Linux_, _MacOS X and Windows_ operating systems.&#x20;

However, since release 4.5, BeeDeeM task engine relies on additional bash shell scripts, making the software capable of running only on Unix-based operating systems (Linux and macOS). Windows users are now invited to run BeeDeeM from the Windows Linux Subsystem.

Finally, BeeDeeM cluster task engine, enabling the software to distribute jobs on computing nodes, is only available for a Linux OS.

## Software

Software dependency of BeeDeeM is as follows, depending on the installation mode:&#x20;

* for legacy installation and use: an [_Oracle Java Runtime Environment_ (JRE)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html), version 1.8 or higher
* for other types of installation: either Docker, Singularity or Anaconda has to be installed on your host system.

## Hardware

Being a bioinformatics databanks manager software, _BeeDeeM_ mostly requires a potentialy huge amont of disk storage; of course, it fully depends on your needs. Generally, the disk space required must be at least twice the size of the databases to be generated. In effect, when _BeeDeeM_ installs a new version of a database, its already installed copy remains available to the users.

## Ressources

BeeDeeM requires at least 4 CPUs, 4 Gb RAM and from half an hour (PDB) up to 48 hours (TrEMBL) to install a databank. Running time depends on network speed, too.

Now, if your bank descriptors (the configuration files telling BeeDeeM how to install banks; see [#what-is-a-databank-descriptor](../getting-started/using-descriptors.md#what-is-a-databank-descriptor "mention")) use external scripts to achieve additional post-processings, higher ressources may be required. As an example, installing TrEMBL with BLAST V4 and V5 bank formats, Diamond and Bowtie2 indexes require up to 32 Go RAM (using 4 CPUs).

