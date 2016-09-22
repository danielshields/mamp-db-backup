# mamp-db-backup
Shell script for backing up all databases to a Dropbox folder

```
/applications/MAMP/library/bin/mysql -s -r -u root -proot -e 'show databases' | egrep -v 'information_schema|performance_schema|mysql|test' | while read db; do /applications/MAMP/library/bin/mysqldump -u root -proot $db -r ~/Dropbox/Databases/${db}.sql; [[ $? -eq 0 ]] ;done
```

### You have to update 2 things to get it to work:
1. Database username / password. By default, these are "root" and "root" in MAMP, but if you've changed them, update ```-u root``` to read ```-u YOURUSERNAME``` and ```-proot``` to read ```-pYOURPASSWORD```.
2. File location is set by default to a "Databases" directory in Dropbox. Update it to point to another directory, or add a directory to make it computer-specific. ```~/Dropbox/Databases/Laptop/${db}.sql```

### Automator as scheduled task
I run the script in OSX Automator because it allows you to attach the script to a repeating calendar event, and run the script on a nightly/weekly/monthly basis.

[Automator Screenshot](automator.png)