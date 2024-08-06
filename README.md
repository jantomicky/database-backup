# database-backup

Bash script(s) for backing up MySQL / MariaDB databases with `mysqldump`, backups are timestamped, archived and optionally pruned based on age. Bash is required as the scripts use Bash specific features.

## Setup

- (Recommended) Create a dedicated read only database user for the backup purposes.
MySQL <=5.7
```
GRANT SHOW DATABASES, SELECT, LOCK TABLES, SHOW VIEW ON *.* TO 'your-user'@'localhost' IDENTIFIED BY 'your-password';
```
MySQL >= 8.0
```
CREATE USER 'your-user'@'%' IDENTIFIED BY 'your-password'; GRANT SHOW DATABASES, SELECT, LOCK TABLES, SHOW VIEW ON *.* TO 'your-user'@'%'; FLUSH PRIVILEGES;
```

- Clone the repo `git clone https://github.com/jantomicky/database-backup.git`
- `cd database-backup/`
- Run `./init` to generate a configuration file and pass your database credentials (which are saved in `$HOME/my.conf`)
  - You can set ENV variables for "no interaction" setup:
    - `DATABASE_BACKUPS_PATH`
    - `DATABASE_BACKUPS_KEEP_FOR_DAYS`
    - `DATABASE_BACKUPS_USERNAME`
    - `DATABASE_BACKUPS_PASSWORD`
- Create a backup by running `./database-backup`
- (Recommended) Setup automatic backups with cron (`crontab -e`):
```
0 22 * * * /path/to/database-backup
```
