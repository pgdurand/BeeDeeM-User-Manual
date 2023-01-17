# Quick start guide

In this section we present the use of BeeDeeM command-line tools whatever the installation you use (legacy, Docker, Singularity or Conda).&#x20;

So, when we say: "use `bdm` tool to do something", you will have to adapt the command-line to conform to your installation. Examples:

* Legacy and Conda installations: you can invoke BeeDeeM tools directly, since path to BeeDeeM tools is added in your PATH environment variable
* Docker: prefix BeeDeeM command-line tool name with: "docker run .../..."
* Singularity: prefix BeeDeeM command-line tool name with: "singularity run .../..."

## BeeDeeM master command

Running BeeDeeM is as simple as using the unique command: `bdm`.

You get help with: `bdm -h` or `bdm --help`.

## BeeDeeM sub-commands

Expected first argument of bdm command is one of the following sub-commands (also called BeeDeeM tools):

| sub-command | description                                                                                   |
| ----------- | --------------------------------------------------------------------------------------------- |
| annot       | annotate a BLAST XML formatted file                                                           |
| check       | check whether or not a descriptor is still ok (URL not broken, etc)                           |
| delete      | delete bank(s)                                                                                |
| desc        | get list of bank descriptors from default conf directory, i.e. ${installDir}/conf/descriptors |
| info        | print out list of installed banks                                                             |
| install     | install bank(s)                                                                               |
| query       | query bank repository to fetch entry(ies) given ID(s)                                         |
| ui          | start bank manager graphical user interface                                                   |

You can easily get an overview of all these tools using such a command:

* `bdm -h`: display available list of tools along with a short description
* `bdm install -h`: display usage of tool `install`



###

__

