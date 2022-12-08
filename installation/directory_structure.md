# Directory structure

Basically, BeeDeeM expects to access two directories for processing banks installation:

* a working directory (_workingDir_): to create log files, temporary files, _etc._
* a bank home directory (_biobaseRootDir_): the place where all banks are installed. Inside that directory, BeeDeeM creates and manages sub-directories... you are invited to avoid editing manually that structure!&#x20;

Of course, BeeDeeM requires read/write permissions on these two directories.

When using the legacy installer, _workingDir_ and _biobaseRootDir_ are set at installation time.

When using either Docker, SIngularity or Conda installation mode, _workingDir_ and _biobaseRootDir_ are set at runtime using KL\_WORKING\_DIR and KL\_mirror\_\_path environment variables, respectively (variable names are case sensitive and there are indeed two underscore characters between "mirror" and "path", this is NOT a typo; more on this later).

