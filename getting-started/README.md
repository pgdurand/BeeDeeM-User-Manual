# BeeDeeM reference manual

## BeeDeeM master command

Running BeeDeeM is as simple as using the unique command: `bdm`.

You get help with: `bdm -h` or `bdm --help`.

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

_Note:_ during BeeDeeM execution, there is nothing displayed on the terminal whether something goes OK or wrong. However, _BeeDeeM_ logs all its work in a dedicated log file located in ${workingDir}.&#x20;
