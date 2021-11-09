#**Backup services SLA**

Descriptions of backup approaches contain information on specific backup attributes, such as:

**Backup coverage** - what is backed up and what is not
**Backup RPO (recovery point objective)** - acceptable data loss (time period)
**Versioning and retention** - how many backup versions are stored and for how long
**Usability** - how is the backup recovery verified (backup should be usable)
**Restoration criteria** - when should backup be restored
**Backup RTO (recovery time objective)** - how long will it take to restore the service

##**Backup coverage**
Backup service covers only the next services:
Database services - **MySQL** and **InfluxDB**. The database services contain user data. Other services in our system such as *Nginx*, *AGAMA*, *Grafana* and *Bind* **do not store any personal or client data** and everything can be re-created from scratch using Ansible playbook.

##**Versioning and retention**
Incremental backups are done automatically every day at 00:35. Incremental backup stores only the difference in the data relative to the last incremental backup.
First incremental backup stores difference from the last created full backup.
Full backups contain all data from services that are backed up and they are done on every 4 weeks (28 days as not all the months have 28+ days).
Backpus are retained for 28 days, only 2 versions can be stored at the same time.
The oldest backup is deleted at 00:40 on the 28th day of every month

##**Usability**
Usability of the last backup is checked every 7 days and tested in  virtual environment setup, simulating our real infrastructure.

##**Restoration criteria**
Backup should be restored if it is known that stored data was lost or deleted.

##**Backup RTO (recovery time objective)**
Backup service should take not more than 2 hours to fully recover the data.
