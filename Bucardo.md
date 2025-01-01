# Create Database Replication Using `Bucardo`

## Prerequisites

- Server with `sudo` access.
- Perl must be installed on the server.
- PostgreSQL must be installed (ensure version compatibility with Bucardo).


## Perl Installation

### Using `apt` Package Manager

Install the required Perl library:

```bash
sudo apt-get install libdbix-safe-perl
```

### Manual Installation

1. Download the `DBIx::Safe` compressed file:

   ```bash
   wget https://bucardo.org/downloads/dbix_safe.tar.gz
   ```

2. Unpack the file and access the directory:

   ```bash
   tar xzf dbix_safe.tar.gz
   cd DBIx-Safe-1.2.5
   ```

3. Install `make`:

   ```bash
   sudo apt install make
   ```

4. Run the `Makefile.PL` script and tests:

   ```bash
   perl Makefile.PL
   make
   make test
   ```

5. Install the package:

   ```bash
   sudo make install
   ```

---

## Bucardo Installation

1. Download Bucardo and extract it:

   ```bash
   wget https://bucardo.org/downloads/Bucardo-5.6.0.tar.gz
   tar xzf Bucardo-5.6.0.tar.gz
   cd Bucardo-5.6.0
   ```

2. Run the `Makefile.PL` script and install Bucardo:

   ```bash
   perl Makefile.PL
   make
   sudo make install
   ```

---

## Create the Bucardo Database

1. Install the PostgreSQL Perl extension:

   ```bash
   sudo apt-get install postgresql-plperl
   ```

2. Start the installation process:

   ```bash
   bucardo install
   ```

3. Fill in the required details during the installation process:
   - Host: `localhost` (if running locally).
   - Port: `5432` (default PostgreSQL port).
   - User: PostgreSQL superuser (e.g., `postgres`).
   - Database: Name for the Bucardo database (e.g., `bucardo`).
   - PID Directory: Directory for Bucardo's PID file (e.g., `/var/run/bucardo`).

4. Example prompt:

   ```plaintext
   This will install the bucardo database into an existing Postgres cluster.
   Postgres must have been compiled with Perl support,
   and you must connect as a superuser.

   We will create a new superuser named 'bucardo',
   and make it the owner of a new database named 'bucardo'.

   Current connection settings:
   1. Host:          <none>
   2. Port:          5432
   3. User:          postgres
   4. Database:      postgres
   5. PID directory: /var/run/bucardo
   ```

---

## Adding Databases to Bucardo

Assume you want to replicate data from `db1` to `db2`.

### Database 1

```bash
bucardo add db db_example_1 dbhost=db1host dbport=db1port dbname=db1name dbuser=db1user dbpass='db1pass'
```

### Database 2

```bash
bucardo add db db_example_2 dbhost=db2host dbport=db2port dbname=db2name dbuser=db2user dbpass='db2pass'
```

---

## Adding Tables and Sequences

### Add All Tables and Sequences to a Herd

```bash
bucardo add all tables --herd=exampleherd
bucardo add all sequences --herd=exampleherd
```

### Remove a Table

```bash
bucardo remove table public.table_name --herd=exampleherd
```

---

## Creating and Managing Syncs

1. **Create a Sync**  
   For example, sync data from `db1` to `db2`:

   ```bash
   bucardo add sync dev_sync herd=exampleherd dbs=db_example_1:source,db_example_2:target onetimecopy=2
   ```

2. **Start the Sync**  

   ```bash
   bucardo start
   ```

3. **Stop the Sync**  

   ```bash
   bucardo stop
   ```

---

## Removing Databases, Tables, or Sequences

### Delete a Sequence

```bash
bucardo remove sequence seqname
bucardo remove sequence seqname --herd=exampleherd
```

### Delete a Database

```bash
bucardo remove db dbname
bucardo remove db dbname --force
```

---

## Uninstalling Bucardo

1. Stop all Bucardo processes:

   ```bash
   bucardo stop
   ```

2. Remove the Bucardo database manually after deleting Bucardo from the system.

---

## Notes

1. **What is a Herd?**  
   A *herd* is a group of tables and sequences used as a target for actions like synchronization.

2. **Directory Creation**:  
   If errors occur during installation, manually create the following directories:

   ```bash
   sudo mkdir -p /var/run/bucardo /var/log/bucardo
   ```

3. **Synchronization Modes**:  
   Bucardo supports two modes of synchronization. Learn more [here](https://bucardo.org/Bucardo/operations/onetimecopy).

---

## Resources

- [Bucardo Documentation](https://bucardo.org/Bucardo)
- [PostgreSQL Replication Using Bucardo 5.4.1 | Medium](https://medium.com/@logeshmohan/postgresql-replication-using-bucardo-5-4-1-6e78541ceb5e)

---Here’s an updated and polished version of your document in Markdown:

# Create Database Replication Using `Bucardo`

## Prerequisites

- Server with `sudo` access.
- Perl must be installed on the server.
- PostgreSQL must be installed (ensure version compatibility with Bucardo).


## Perl Installation

### Using `apt` Package Manager

Install the required Perl library:

```bash
sudo apt-get install libdbix-safe-perl
```

### Manual Installation

1. Download the `DBIx::Safe` compressed file:

   ```bash
   wget https://bucardo.org/downloads/dbix_safe.tar.gz
   ```

2. Unpack the file and access the directory:

   ```bash
   tar xzf dbix_safe.tar.gz
   cd DBIx-Safe-1.2.5
   ```

3. Install `make`:

   ```bash
   sudo apt install make
   ```

4. Run the `Makefile.PL` script and tests:

   ```bash
   perl Makefile.PL
   make
   make test
   ```

5. Install the package:

   ```bash
   sudo make install
   ```

---

## Bucardo Installation

1. Download Bucardo and extract it:

   ```bash
   wget https://bucardo.org/downloads/Bucardo-5.6.0.tar.gz
   tar xzf Bucardo-5.6.0.tar.gz
   cd Bucardo-5.6.0
   ```

2. Run the `Makefile.PL` script and install Bucardo:

   ```bash
   perl Makefile.PL
   make
   sudo make install
   ```

---

## Create the Bucardo Database

1. Install the PostgreSQL Perl extension:

   ```bash
   sudo apt-get install postgresql-plperl
   ```

2. Start the installation process:

   ```bash
   bucardo install
   ```

3. Fill in the required details during the installation process:
   - Host: `localhost` (if running locally).
   - Port: `5432` (default PostgreSQL port).
   - User: PostgreSQL superuser (e.g., `postgres`).
   - Database: Name for the Bucardo database (e.g., `bucardo`).
   - PID Directory: Directory for Bucardo's PID file (e.g., `/var/run/bucardo`).

4. Example prompt:

   ```plaintext
   This will install the bucardo database into an existing Postgres cluster.
   Postgres must have been compiled with Perl support,
   and you must connect as a superuser.

   We will create a new superuser named 'bucardo',
   and make it the owner of a new database named 'bucardo'.

   Current connection settings:
   1. Host:          <none>
   2. Port:          5432
   3. User:          postgres
   4. Database:      postgres
   5. PID directory: /var/run/bucardo
   ```

---

## Adding Databases to Bucardo

Assume you want to replicate data from `db1` to `db2`.

### Database 1

```bash
bucardo add db db_example_1 dbhost=db1host dbport=db1port dbname=db1name dbuser=db1user dbpass='db1pass'
```

### Database 2

```bash
bucardo add db db_example_2 dbhost=db2host dbport=db2port dbname=db2name dbuser=db2user dbpass='db2pass'
```

---

## Adding Tables and Sequences

### Add All Tables and Sequences to a Herd

```bash
bucardo add all tables --herd=exampleherd
bucardo add all sequences --herd=exampleherd
```

### Remove a Table

```bash
bucardo remove table public.table_name --herd=exampleherd
```

---

## Creating and Managing Syncs

1. **Create a Sync**  
   For example, sync data from `db1` to `db2`:

   ```bash
   bucardo add sync dev_sync herd=exampleherd dbs=db_example_1:source,db_example_2:target onetimecopy=2
   ```

2. **Start the Sync**  

   ```bash
   bucardo start
   ```

3. **Stop the Sync**  

   ```bash
   bucardo stop
   ```

---

## Removing Databases, Tables, or Sequences

### Delete a Sequence

```bash
bucardo remove sequence seqname
bucardo remove sequence seqname --herd=exampleherd
```

### Delete a Database

```bash
bucardo remove db dbname
bucardo remove db dbname --force
```

---

## Uninstalling Bucardo

1. Stop all Bucardo processes:

   ```bash
   bucardo stop
   ```

2. Remove the Bucardo database manually after deleting Bucardo from the system.

---

## Notes

1. **What is a Herd?**  
   A *herd* is a group of tables and sequences used as a target for actions like synchronization.

2. **Directory Creation**:  
   If errors occur during installation, manually create the following directories:

   ```bash
   sudo mkdir -p /var/run/bucardo /var/log/bucardo
   ```

3. **Synchronization Modes**:  
   Bucardo supports two modes of synchronization. Learn more [here](https://bucardo.org/Bucardo/operations/onetimecopy).

---

## Resources

- [Bucardo Documentation](https://bucardo.org/Bucardo)
- [PostgreSQL Replication Using Bucardo 5.4.1 | Medium](https://medium.com/@logeshmohan/postgresql-replication-using-bucardo-5-4-1-6e78541ceb5e)

---
