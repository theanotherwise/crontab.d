# Separated cron files..

## Benefits
 * separated script per service/program/type/etc.
 * creating log file from runned script with `.log` file extension
 * errors/problems of scripts log to `.log` file (2>&1)
 
## How to use?
 * be sure when use `>`, `>>`, example:
   * script run once time per day `>` 
   * script run many times per day `>>` (care disk space)

## Structure 
```bash
mkdir -p /root/crontab.d
mkdir -p /root/crontab.d/system
mkdir -p /root/crontab.d/apache2

touch /root/crontab.d/system.cron
touch /root/crontab.d/system/alpha.sh
touch /root/crontab.d/system/beta.sh

touch /root/crontab.d/apache2.cron
touch /root/crontab.d/apache2/stop.sh
touch /root/crontab.d/apache2/start.sh

find /root/crontab.d -type d -exec chmod 700 {} \;
find /root/crontab.d -type f -exec chmod 600 {} \;
```

# Cron files

```bash
# /root/crontab.d/system.cron
*/1 * * * * /bin/bash /root/crontab.d/system/log.sh >> /root/crontab.d/system/log.log 2>&1
*/1 * * * * /bin/bash /root/crontab.d/system/test.sh >> /root/crontab.d/system/test.log 2>&1
```

```
# /root/crontab.d/apache2.cron
30 1 * * * /bin/bash /root/crontab.d/apache2/stop.sh > /root/crontab.d/apache2/stop.log 2>&1
31 1 * * * /bin/bash /root/crontab.d/apache2/start.sh > /root/crontab.d/apache2/start.log 2>&1
```
