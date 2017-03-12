# Common errors and solutions

The various uses that have been made of *BeeDeeM* have shown that processing errors very often result from problems related to the FTP connections with the remote systems. Although *BeeDeeM* uses a system of restarting on connection errors, this system finally abandons connections causing to many recurrent errors. In this case, *BeeDeeM* places an error message in its log file. 

## Error when loading the remote file list

The first processing step performed by *BeeDeeM* to download a sequence database consists of retrieving the list of files that must be retrieved from a remote system. 

The following error shows a connection failure with an FTP server:

    WARN  KFTPLoader  | Error during FTP listing: org.apache.commons.net.ftp.FTPConnectionClosedException: Connection closed without indication.
    WARN  KFTPLoaderSystem  | Failed to retrieve files list for db: gbcore_data

**Problem analysis:**

For an unknown reason, the remote system has closed the FTP session. In this case, *BeeDeeM* was not able to read the data it needed, i.e. the list of files that it should download.

**Solution:**

This error corrects itself when restarting *BeeDeeM* in restart after failure mode (c.f. Restart on failure). 

## File load error

The following error shows a load failure for a file during an FTP connection:

    INFO  KFTPLoader  | Connected to ftp.ncbi.nlm.nih.gov: 230
    INFO  KFTPLoader  |   download: /genbank/gbpat26.seq.gz
    WARN  KFTPLoader  | Error during FTP download: org.apache.commons.net.io.CopyStreamException: IOException caught while copying.
    INFO  KFTPLoaderSystem  | Download status for: gbpat26.seq.gz: failure

**Problem analysis:**

The first two lines of this *BeeDeeM* log extract show that it correctly started a download of the Genbank file gbpat26.seq.gz. However, an I/O error occurred and *BeeDeeM* informs us that this file could not be downloaded.

**Solution:**

This error corrects itself when restarting *BeeDeeM* in restart after failure mode (c.f. Restart after failure). 


## Task execution error

*BeeDeeM* uses a wait file to execute its various tasks. These are organised into unit tasks (applied to specific downloaded files) and global tasks (applied to all downloaded files). For example, unit tasks are: download, decompression, unarchiving and indexing. Among the global tasks, there are operations on files and directories: delete files and rename a directory, for example. For more information about the task system, please consult the *BeeDeeM* User Interface Manual.

### Unit task error

The following log file extract shows the case of an error in decompressing a ‘gzip’ file:

    INFO  KFTPLoader  | Connected to ftp.ncbi.nlm.nih.gov: 230
    INFO  KFTPLoader  |   download: /blast/db/nt.01.tar.gz
    WARN  KLAntTasks  | Unable to execute gunzip: Problem expanding gzip Unexpected end of ZLIB input stream
    WARN  KLTaskEngine  | Unable to execute task: gunzip: unable to gunzip /biobase/nucleic/blast/nt/20071101/nt/nt.00.tar.gz

**Problem analysis:**

The first two lines show us that *BeeDeeM* downloaded a file of type ‘tar.gz’. Apparently, the download went well. However, the first ‘WARN’ line alerts us of the possibility that we have downloaded an incomplete GZIP file. To verify this hypothesis, you simply compare the size of the remote file (as indicated in the log file) with that of the file on the local disk. And, in our case, the local file nt.01.tar.gz is indeed incomplete.

**Solution:**

This error is corrected by deleting all the contents of the installation directory (in our example: /biobase/nucleic/blast/nt/20071101/nt) and restarting *BeeDeeM* in restart after failure mode (c.f. 6.1.Restart after failure). 

### Global task error

Above we gave an example of the failure of a unit task (decompression of a file). In the same way, global tasks can fail and, in all cases, they do not execute if a unit task has failed. Continuing our previous example, we see the following line in the log file:

    WARN  KLTaskEngine  | Unable to execute task: delfiles: unable to delete files: warn messages emitted.

**Problem analysis:**

This log file line is produced after the decompression task for file nt.01.tar.gz. It is therefore normal to see the refusal to execute the ‘delfiles’ task which is a global task.

**Solution:**

This type of global task execution error is self-correcting when all of the unit tasks are correctly performed.