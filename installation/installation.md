# Installation

## Legacy vs modern installations

BeeDeeM software development started in early February 2007. To provide a multi-OS, open source and free software installer at that time, the [Apache Ant tool ](https://ant.apache.org/)was chosen. This is called the _legacy BeeDeeM installer_.&#x20;

Over time, modern installation procedures were provided relying on Docker, Singularity and Conda. Today, these are the recommanded ways of installing BeeDeeM.

## Docker

You can run _BeeDeeM_ within a Docker container, as explained in [this documentation](https://github.com/pgdurand/BeeDeeM/tree/master/docker).&#x20;

* _Pros_ of Docker configuration: direct use.&#x20;
* _Cons_ of Docker:&#x20;
  * not always easy to use on particular clusters,&#x20;
  * benefit from all BeeDeeM features, but the [UiInstaller](../getting-started-1/).&#x20;

## Singularity

You can run _BeeDeeM_ within a Singularity container, as explained in [this documentation](https://github.com/pgdurand/BeeDeeM/tree/master/singularity).&#x20;

* _Pros_ of Singularity configuration: direct use.&#x20;
* _Cons_ of Singularity:&#x20;
  * benefit from all BeeDeeM features, but the [UiInstaller](../getting-started-1/).&#x20;

## Conda

Finally, you can install and run BeeDeeM using Anaconda tool as explained in [this documentation](https://anaconda.org/SeBiMER/beedeem). You can benefit from all BeeDeeM features, including the [UiInstaller](../getting-started-1/).&#x20;

## Legacy installation

You can install the software directly on a computer (or server, or cluster, ...) to benefit from **ALL** its features, including the use of the [UiInstaller](../getting-started-1/). The following section explains how to do that.

It only requires the file **beedeem-x.y.z-distrib.zip** (where x.y.z is a version number) which contains the entire _BeeDeeM_ system.

By default, the _BeeDeeM_ installation procedure will pre-configure your system to manage some default sequence databanks and ontologies. More can be installed later on.

### Download and extract _BeeDeeM_

We consider an installation on a Unix-based system (Linux, macOS), but you can easily adapt for Windows OS.

_BeeDeeM_ is available on Github [here](https://github.com/pgdurand/BeeDeeM/releases).

Then proceed as follows:

**-1-** Prepare a temporary directory from which the installation will be performed:

```
cd /tmp
mkdir dbms
cd dbms
```

place the dbmanager-x.y.z-distrib.zip file in the directory /tmp/dbms.

**-2-** Decompress the file beedeem-x.y.z-distrib.zip:

```
unzip beedeem-x.y.z-distrib.zip
```

**-3-** Check if _Oracle Java_ and _Apache Ant_ are available on your system:

```
java -version
   java version "1.8.0_45"
   Java(TM) SE Runtime Environment (build 1.8.0_45-b14)
   Java HotSpot(TM) 64-Bit Server VM (build 25.45-b02, mixed mode)

ant -version
   Apache Ant(TM) version 1.10.3 compiled on March 24 2018
```

If _Java_ and _Ant_ are already installed and available on your system, jump to step 5, below.

If _Java_ is not available, please proceed to the web site of [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) to install the _Java Runtime Environment_. **DO NOT use OpenJDK, gcj, etc**. _BeeDeeM_ only works well with the original _Oracle Java_.

Decompress the _Ant_ system supplied with _BeeDeeM_:

```
cd ant
unzip  ant-1.9.4.zip
cd bin
chmod a+x ant antRun
cd ../..
```

### Setup the _BeeDeeM_ configuration

**-4-** Declare your system configuration.

You have now to define:

* the directories used by the _BeeDeeM_ installer to correctly deploy it on your system (_c.f._ [Directory structure](directory\_structure.md)):&#x20;
  * installation directory: where BeeDeeM will be deployed,&#x20;
  * working directory: where BeeDeeM can create temporary files,
  * bank installation directory: where BeeDeeM will install banks;
* the memory parameters to use with _JRE_.

To do that, edit the file **config.properties**. This contains documentation explaining how it should be modified.

```
vi config.properties [update file as needed]

installDir=/opt/beedeem          <-  Installation directory
workingDir=/var/beedeem          <-  Working directory
biobaseRootDir=/biobase          <-  Where to install databases
javaArgs=-Xms128M -Xmx1024M      <-  JRE memory settings

(After editing, save config.properties file)
```

<mark style="color:red;">**CAUTION**</mark>: have in mind that during installation, directories targeted by `installDir`will be DELETED (only if they exist) then created by the software installer; _e.g._ in the above example, /opt/beedeem is deleted then created again by BeeDeeM installer.

It is worth noting that all these values can be updated after installation, but in a less easier way. So carefully choose your installation directories by now.

### Start the installation

It is now time to install _BeeDeeM_:

```
ant -f deploy.xml install
```

On start-up, the _BeeDeeM_ installer will ask you to verify your system configuration:

`Buildfile: deploy.xml`\
`install:` \
&#x20;   `[echo] *** PLEASE VERIFY ***` \
&#x20;   `[echo]` \
&#x20;   `[echo]` \
&#x20;   `[echo] Current configuration is:` \
&#x20;   `[echo] Installation dir: /opt/beedeem` \
&#x20;   `[echo] Working dir : /var/beedeem` \
&#x20;   `[echo] BioBase dir : /biobase` \
&#x20;   `[echo] Java args : -Xms128M -Xmx4G` \
&#x20;   `[input] If ok, press Return key to start the installation...`

Do not omit this step: this is the last time you can perform this verification.&#x20;

In the case of an error, you can interrupt the installation with CTRL+C. Otherwise, continue with this procedure.

Carefully check the final message from _Ant._ If everything is correct, you should see the message:

```
 BUILD SUCCESSFUL
```
