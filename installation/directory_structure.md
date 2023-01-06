# Directory structure

Basically, BeeDeeM expects to access two directories for processing banks installation at runtime:

* a working directory (_workingDir_): to create log files, temporary files, _etc._
* a bank home directory (_biobaseRootDir_): the place where all banks are installed. Inside that directory, BeeDeeM creates and manages sub-directories... you are invited to avoid editing manually that structure!&#x20;

_Note_: when using the legacy or Conda installer, there is a third directory, refer to as _installDir_, where BeeDeeM software has been installed. More on this in the next section.

Of course, BeeDeeM requires read/write permissions on _workingDir and biobaseRootDir_ directories.

When using the legacy installer, _workingDir_ and _biobaseRootDir_ are set at installation time.

When using either Docker, Singularity or Conda installation mode, _workingDir_ and _biobaseRootDir_ are set at runtime using KL\_WORKING\_DIR and KL\_mirror\_\_path environment variables, respectively (variable names are case sensitive and there are indeed two underscore characters between "mirror" and "path", this is NOT a typo; more on this later).

