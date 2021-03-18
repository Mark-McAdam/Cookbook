```
tail -f /var/log/syslog | grep CRON
```

or 

```
whereis syslog
```

or 

```
tail -f $(whereis syslog) | grep CRON
```
