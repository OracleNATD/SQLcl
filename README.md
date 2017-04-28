# SQLcl

[SQLcl](http://www.oracle.com/technetwork/developer-tools/sqlcl/overview/index.html) caught my attention because it's now supported in [Oracle's Developer Cloud Service](https://cloud.oracle.com/developer_service)(See [Adding a Build Step that Invokes SQLcl](http://docs.oracle.com/en/cloud/paas/developer-cloud/csdcs/managing-project-jobs-and-builds-oracle-developer-cloud-service.html#GUID-9D31DDA7-2EB8-496E-9228-2588F636CE84)). Investigating further, it appears to address all the shortcomings of SQL\*Plus as SQLcl provides in-line editing, statement completion, and command recall for a feature-rich experience, all while also supporting your previously written SQL*Plus scripts. 

## Getting Started
SQLcl is only included with 12.2 Database Cloud Service instances. Here's how I got it up and running on a 12.1 instance.
- [Download](http://www.oracle.com/technetwork/developer-tools/sqlcl/downloads/index.html) SQLcl to your workstation
- SCP the zip to the oracle home directory of your Database Cloud instance
- Extract the archive
- SQLcl requires Java 8, so edit the /home/oracle/.bashrc and add the following 2 lines to the bottom to set the JAVA_HOME, SQLCL_HOME and update the PATH:
```
export JAVA_HOME=/u01/app/oracle/product/java/jdk1.8.0_74
export SQLCL_HOME=/home/oracle/sqlcl
export PATH=$JAVA_HOME/bin:$SQLCL_HOME/bin:$PATH

```
Then source your new .bashrc, verify your Java version and test running SQLcl:
```
[oracle@DevOpsDB ~]$ . .bashrc
[oracle@DevOpsDB ~]$ java -version
java version "1.8.0_74"
Java(TM) SE Runtime Environment (build 1.8.0_74-b02)
Java HotSpot(TM) 64-Bit Server VM (build 25.74-b02, mixed mode)
[oracle@DevOpsDB ~]$ sql

SQLcl: Release 4.2.0 Production on Wed Mar 29 19:02:01 2017

Copyright (c) 1982, 2017, Oracle.  All rights reserved.

Username? (''?)

```
Some useful commands:


```
SQL> [oracle@DevOpsDB ~]$ sql / as sysdba

Error starting at line : 1 in command -
[oracle@DevOpsDB ~]$ sql / as sysdba
Error report -
Unknown Command

SQL>
```

```
[oracle@DevOpsDB ~]$ sql DEVOPS/DEVOPS@PDB1

SQLcl: Release 4.2.0 Production on Fri Apr 28 13:51:39 2017

Copyright (c) 1982, 2017, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning and Real Application Testing options


SQL> 
```

```
[oracle@DevOpsDB ~]$ sql sys/{password}@pdb1 as sysdba;

SQLcl: Release 4.2.0 Production on Fri Apr 28 13:58:14 2017

Copyright (c) 1982, 2017, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning and Real Application Testing options


SQL>
```