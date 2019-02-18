# Installation

## Docker

You can run _BeeDeeM_ within a Docker container, as explained in [this documentation](https://github.com/pgdurand/BeeDeeM/tree/master/docker). _Pros_ of Docker configuration: direct use. _Cons_ of Docker: you won't be able to use the [UiInstaller](/ui/getting-started.md).

## Local / Server / Cluster

You can install the software on your own computer \(or server, or cluster, ...\) to benefit from **ALL** its features, including the use of the [UiInstaller](/ui/getting-started.md). The following manual explains how to do that.

The _BeeDeeM_ install procedure has to be executed by a system administrator.

It only requires the file **beedeem-x.y.z-distrib.zip** \(where x.y.z is a version number\) which contains the entire _BeeDeeM_ system.

By default, the _BeeDeeM_ installation procedure will pre-configure your system to manage some default sequence databanks and ontologies. More can be installed later on.

## Download and extract _BeeDeeM_

We consider an installation on a Unix-based system \(Linux, MacOS X\), but you can easily adapt for Windows OS.

_BeeDeeM_ is available on Github [here](https://github.com/pgdurand/BeeDeeM/releases).

Open a ‘root’ session in a terminal window.

Then proceed as follows:

**-1-** Prepare a temporary directory from which the installation will be performed:

```
$ cd /tmp
$ mkdir dbms
$ cd dbms
```

place the dbmanager-x.y.z-distrib.zip file in the directory /tmp/dbms.

**-2-** Decompress the file beedeem-x.y.z-distrib.zip:

```
$ unzip beedeem-x.y.z-distrib.zip
```

**-3-** Check if _Oracle Java_ and _Apache Ant_ are available on your system:

```
$ java -version
java version "1.8.0_45"
Java(TM) SE Runtime Environment (build 1.8.0_45-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.45-b02, mixed mode)

$ ant -version
Apache Ant(TM) version 1.10.3 compiled on March 24 2018
```

If _Java_ and _Ant_ are already installed and available on your system, jump to step 5, below.

If _Java_ is not available, please proceed to the web site of [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) to install the _Java Runtime Environment_. **DO NOT use OpenJDK, gcj, etc**. _BeeDeeM_ only works well with the original _Oracle Java_.

If _Ant_ is not available on your computer, decompress the _Ant_ system supplied with _BeeDeeM_:

```
$ cd ant/bin
$ chmod a+x ant antRun
$ cd ../..
```

## Setup the _BeeDeeM_ configuration

**-4-** Prepare some environment variables to tell the _BeeDeeM_ installer where to find _Ant_ and the _Java Runtime_.

**Note**: if _Java_ and _Ant_ are already installed and available on your system, jump to step 5.

This information is given in the file **envDBMS** which you should edit and correctly update. If you choose to use the _Ant_ system supplied with _BeeDeeM_ \(see step 3, above\), do not modify the declaration of the variable ANT\_HOME in the **envDBMS** file:

```
$ vi envDBMS     [update file as needed]

#  Provide here the path to the home directory of an
#  Oracle JRE release 1.8 or above
#
JAVA_HOME=/usr/local/jre1.8      <-- UPDATE AT LEAST THIS LINE
.../...
```

After editing, save envDBMS file, then:

```
$ source envDBMS
```

**-5-** Declare your system configuration.

You have now to define:

* the directories used by the _BeeDeeM_ installer to correctly deploy it on your system \(_c.f._ [Directory structure](directory_structure.md)\),
* the _JRE_ home directory,
* the memory parameters to use with _JRE_.

To do that, edit the file **config.properties**. This contains documentation explaining how it should be modified.

```
$ vi config.properties [update file as needed]

installDir=/opt/beedeem          <-  Installation directory
workingDir=/var/beedeem          <-  Working directory
biobaseRootDir=/biobase          <-  Where to install databases
javaDir=/usr/java/jre1.6         <-  Home directory of the JRE
javaArgs=-Xms128M -Xmx1024M      <-  JRE memory settings

(After editing, save config.properties file)
```

It is worth noting that all these values can be updated after installation, but in a less easier way. So carefully choose your installation directories by now.

## Start the installation

It is now time to install _BeeDeeM_:

```
$ ant -f deploy.xml install
```

On start-up, the _BeeDeeM_ installer will ask you to verify your system configuration.

Do not omit this step: this is the last time you can perform this verification. In the case of an error, you can interrupt the installation with CTRL+C. Otherwise, continue with this procedure.

Carefully check the final message from _Ant._ If everything is correct, you should see the message:

```
 **BUILD SUCCESSFUL**
```
