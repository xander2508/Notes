SQL Plus is the most basic Oracle Database utility, with a basic command-line interface, commonly used by users, administrators, and programmers.

## Installation

See [[Oracle Database Attacking Tool (ODAT)#Installation]]

## Commands 

There are many [SQLplus commands](https://docs.oracle.com/cd/E11882_01/server.112/e41085/sqlqraa001.htm#SQLQR985) that we can use to enumerate the database manually.
## Usage 

#### Connection 

Where `XE` is a found `SID` and the username/password is `scott` and `tiger`.

```shell-session
sqlplus scott/tiger@10.129.204.235/XE
```

If you come across the following error `sqlplus: error while loading shared libraries: libsqlplus.so: cannot open shared object file: No such file or directory`, please execute the below, taken from [here](https://stackoverflow.com/questions/27717312/sqlplus-error-while-loading-shared-libraries-libsqlplus-so-cannot-open-shared).

```shell-session
sudo sh -c "echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf";sudo ldconfig
```
### Enumeration

#### User Privilege

```shell-session
select table_name from all_tables;
```

```shell-session
select * from user_role_privs;
```

