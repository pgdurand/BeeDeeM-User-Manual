# BeeDeeM configuration

## _BeeDeeM_ installation directory

Whatever the installation used, BeeDeeM is located within a directory, hereafter calle _${installDir}_.

The _BeeDeeM_ directory _${installDir}_ is organised as follows (Linux/OSX defaults):

| Directory                | Content                                                                                                                                   | Default value                    |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
| _${installDir}_          | Home directory of _BeeDeeM_                                                                                                               | /opt/beedeem  (1)                |
| _${installDir}/bin_      | Java libraries for _BeeDeeM_ and its dependencies                                                                                         | _${installDir}_/bin              |
| _${installDir}/external_ | Native binaries (such as makeblastdb) for Linux, MacOSX or Windows                                                                        | _${installDir}_/external         |
| _${descriptors}_         | Directory containing particular files called: **databank descriptor files**. These files instruct the software how to install databanks.  | _${installDir}_/conf/descriptors |
| ${scripts)               | Databank descriptors additional pre- and post-processing tasks                                                                            | _${installDir}_/conf/scripts     |

(1) Default values for Legacy, Docker or Singularity installation ; Conda may use a different path.

## BeeDeeM additional directories

| Directory           | Description                                                                                                  | Default value                          |
| ------------------- | ------------------------------------------------------------------------------------------------------------ | -------------------------------------- |
| ${_biobaseRootDir}_ | The place where all banks are installed. Inside that directory, BeeDeeM creates and manages sub-directories. | See "Master configuration file", below |
| ${_workingDir_}     | Used by BeeDeeM to create log files, temporary files, _etc._                                                 | See "Working directory", below         |



## Master configuration file

By default, _BeeDeeM_ is configured by a master configuration file located in _${installDir}/conf:_ **dbms.config**. Content of this file is setup during software installation. This text file contents a set of key/value pairs and is documented, so quite easy to understand.

Actually, there is a single very important key/value to look at : `mirror.path`. That key defines the path to ${_biobaseRootDir}. +_

You have three options to (re)define the value associated to that key:

* by editing dbms.config; suitable for legacy installation, it is more difficult to use that solution for any other installations of BeeDeeM, i.e. Conda, Docker or Singularity;
* by setting JRE argument `KL_mirror.path`(1); \
  &#x20;e.g. by editing `bdm` master command-line script and setting: \
  `java .../... -DKL_mirror.path=/a/new/path/to/bank/repository`
* by setting `KL_mirror__path` (2) environment variable; \
  e.g. for bash shell: `export KL_mirror__path=/a/new/path/to/bank/repository`

&#x20;    _(1) variable names are case sensitive;_\
&#x20;    _(2) there are indeed two underscore characters between "mirror" and "path", this is NOT a typo._

The latter solution is realy the most recommended one to use with Conda, Docker or Singularity installation of BeeDeeM.

It is worth noting that environment variable declaration takes priority over JRE -D declaration that takes priority over dbms.config file declaration.

## Working directory

_BeeDeeM_ relies on a dedicated directory to store all its working files: log files, temporary files, etc. By default, that directory is set within `bdm` master command script file (located in _${installDir}_) by variable: `KL_WORKING_DIR`.

You can change the location of that directory at any time using the following declaration (bash shell) before starting BeeDeeM:

&#x20;    `export KL_WORKING_DIR=/a/new/path/to/workdir`.

## Additional configuration controls

Additional `KL_` prefixed variable names exist to easity setup BeeDeeM. As for `KL_mirror__path` and `KL_WORKING_DIR`, these additional `KL_` variables can be setup using one of:

* `export KL_XXX=a_value`
* `java .../... -DKL_XXX=a_value`

And again, shell variable declaration takes priority over JRE -D declaration.

### Log file

The following variables control the creation of BeeDeeM log files:

| Variable      | Role                          | Default                                                       |
| ------------- | ----------------------------- | ------------------------------------------------------------- |
| KL\_LOG\_TYPE | one of: none, console or file | file                                                          |
| KL\_LOG\_FILE | name of log file              | If not set, BeeDeeM creates a log file using sub-command name |
| KL\_DEBUG     | one of: true or false         | false                                                         |

### Configuration directory

By default, BeeDeeM locates bank descriptors in _${descriptors} (see above)._ In case you would like to use your own configuration directory (e.g. containing new bank descriptors), you can tell BeeDeeM to use that directory as follows:

`KL_CONF_DIR=/path/to/new/conf_dir`&#x20;

Such a path must target all expected configuration sub-directories: system, scripts, descriptors. The very easy way to achieve that consists in copying the standard BeeDeeM "conf" directory, then update that copy to meet your needs.

