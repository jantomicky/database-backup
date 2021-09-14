# database-backup

Bash script(s) for backing up MySQL / MariaDB databases with `mysqldump`, backups are timestamped, archived and optionally pruned based on age.

## Setup

- (Recommended) Create a dedicated read only database user for the backup purposes:
```
GRANT SELECT, LOCK TABLES ON *.* TO 'your-user'@'localhost' IDENTIFIED BY 'your-password';
```
- Clone the repo `git clone https://github.com/jantomicky/database-backup.git`
- `cd database-backup/`
- Run `./init` to generate a configuration file and pass your database credentials (which are saved in `$HOME/my.conf`)
- Create a backup by running `./database-backup`
- (Recommended) Setup automatic backups with cron (`crontab -e`):
```
0 22 * * * /path/to/database-backup
```
