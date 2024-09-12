# Create database replication using `bucardo`

# Prerequisites

- Server with `sudo` access
- Perl must be installed on the server
- Postgres must be installed

# Perl Installation

## Using apt package manager

1. install `perl`

```bash
apt-get install libdbix-safe-perl
```

## Manual installation

1. Download `DBIX::Safe` compressed file

```bash
wget https://bucardo.org/downloads/dbix_safe.tar.gz
```

1. Unpack file then access it 
 

```bash
tar xzf dbix_safe.tar.gz
cd DBIx-Safe-1.2.5
```

1. Install make

```bash
sudo apt install make
```

1. Run [`Makefile.PL`](http://Makefile.PL) then run test

```bash
perl Makefile.PL
make
make test
```

1. Install with `make`

```bash
sudo make install
```

# Installation

1. Download `Bucardo` software then open directory

```bash
wget https://bucardo.org/downloads/Bucardo-5.6.0.tar.gz
tar xzf Bucardo-5.6.0.tar.gz
cd Bucardo-5.6.0
```

1. Run [`Makefile.PL`](http://Makefile.PL) then use `make` 

```bash
perl Makefile.PL
make
sudo make install
```

# Create bucardo database

1. Install `postgres` package with perl

```bash
apt-get install postgresql-plperl # Note: use version compatible with pg version
```

1. Start installation

```bash
bucardo install
```

1. Fill information that match needs for database setup, for example
database running locally so host will be: localhost, and port by default will be 5432
user will be dbuser, database will be bucardo, PID directory is the directory that is bucardo located in, so lets assume it is on this directory /home/userx/bucardo/Bucardo-5.6.0
output will be like this, and should be updated interactively 

```bash
This will install the bucardo database into an existing Postgres cluster.
Postgres must have been compiled with Perl support,
and you must connect as a superuser

We will create a new superuser named 'bucardo',
and make it the owner of a new database named 'bucardo'

Current connection settings:
1. Host:          <none>
2. Port:          5432
3. User:          postgres
4. Database:      postgres
5. PID directory: /var/run/bucardo
```

# Adding databases to Bucardo

If we want to replicate data from db1 which has these info

```bash
host=db1host
port=db1port
user=db1user
pass=db1pass
```

to db2 which has these info

```bash
host=db2host
port=db2port
user=db2user
pass=db2pass
```

## Adding database 1

```bash
bucardo add db db_example_1 dbhost=db1host dbport=db1port dbname=db1name dbuser=db1user dbpass='db1pass'
```

## Adding database 2

```bash
bucardo add db db_example_2 dbhost=db2host dbport=db2port dbname=db2name dbuser=db2user dbpass='db2pass'
```

## Adding all tables

We must add tables and sequences

```bash
bucardo add all tables --herd=exampleherd
bucardo add all sequences --herd=exampleherd
```

If we want to remove tables we can use this command, assuming it is in public schema and named
table_name

```bash
bucardo remove table public.table_name --herd=exampleherd
```

## Creating sync

Lets assume we create sync from db1 to db2 then we use this command named `dev_sync` 

```bash
bucardo add sync dev_sync herd=exampleherd dbs=db_example_1:source,db_example_2:target onetimecopy=2
```

## Start sync

```bash
bucardo start
```

# Notes

- What is `herd` ? a `herd` is a group of tables, sequences that used as a filter to target that group when do some action
- You must create directories manually for logging, so when error thrown while you create bucardo database, handle it manually by creating directories if error thrown, these directories are

```bash
/var/run/bucardo
/var/log/bucardo
```

- There are 2 modes for sync and you can know more about them [here](https://bucardo.org/Bucardo/operations/onetimecopy)

# Stop sync

This command used to stop sync between databases

```bash
bucardo stop
```

# Delete sequence from bucardo

```bash
bucardo remove sequence seqname
```

If this sequence is in herd then we specify the herd

```bash
bucardo remove sequence seqname --herd=exampleherd
```

# Delete database from bucardo

```bash
bucardo remove db dbname
```

If this database has tables or sequences then we will do this with `--force`  like this

```bash
bucardo remove db dbname --force
```

# Uninstall Bucardo

# Notes

- You have to delete bucardo database after deleting bucardo from system

# Resources

https://bucardo.org/Bucardo

[PostgreSQL Replication using Bucardo 5.4.1 | by Logesh Mohan | Medium](https://medium.com/@logeshmohan/postgresql-replication-using-bucardo-5-4-1-6e78541ceb5e)