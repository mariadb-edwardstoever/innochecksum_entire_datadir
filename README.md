# Innochecksum Entire Datadir

## Look for possible corruption in each datafile in the Mariadb datadir.

This script will scan the datadir of the Mariadb database and verify each datafile. 

This script can be run while the database is running and in use, however accurate results will be achieved if run when the database is shutdown.

In database releases that include the feature allowing ibdata1 shrinkage, the script will report that ibdata1 is "BAD" even when it is "OK" if the script is run while the database is running.
See 
https://jira.mariadb.org/browse/MDEV-14795
https://jira.mariadb.org/browse/MENT-1304
Known effected versions: 10.6.19, 11.2.1, 10.11.10 


Example of running the script for a support ticket:
```
./innochecksum_entire_datadir.sh | tee /tmp/$(hostname)_innochecksum_entire_datadir.log
```
Attach the created log file to the support ticket.

Output sample finding a bad file:
```
OK      /var/lib/mysql/CS0725679/tbl_menu.ibd
BAD!!   /var/lib/mysql/CS0725679/xyz.ibd
OK      /var/lib/mysql/student_db/std_admissions_schools.ibd
OK      /var/lib/mysql/student_db/another_t.ibd
```
