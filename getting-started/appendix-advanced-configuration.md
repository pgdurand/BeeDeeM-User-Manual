# Appendix - Advanced configuration

## Setup a "_BeeDeeM_" user

It is advised to create a user, such as ‘dbms’, that will be used to manage databank installation instead of using root for such tasks.

As soon as you have created such a user, update file owner and permissions (we suppose that user ‘dbms’ has been created, and that it is member of group ‘user’) :

```
$ chown –R dbms:user ${installDir}
$ chown –R dbms:user ${biobaseRootDir}
$ chown –R dbms:user ${workingDir}

where ${installDir} is the directory where BeeDeeM is installed, 
      ${biobaseRootDir} is the directory where databanks will be stored on your system 
      ${workingDir} is the working directory of BeeDeeM.
```

It is worth noting that ‘dbms:user’ must have read/write access to all files located in _${installDir}_, _${biobaseRootDir}_ and _${workingDir}_. Please check file/directory permissions on these directories.

## Proxy settings

If you need to use a proxy to access to the Internet, update the file called ‘**network.config**’ located within the directory _${installDir}/conf_. The configuration file is self-documented; mainly, you have to setup values for variable _proxy.host_ and _proxy.port_, then set to ‘true’ variable _proxy.use_.
