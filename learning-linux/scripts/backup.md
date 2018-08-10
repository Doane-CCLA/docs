
```bash
#!/bin/bash

SRC_DIR="/Users/user/Documents/my_work/"

DEST_DIR="/Users/user/Backups/"

FILENAME=Backup-$(date +%-Y%-m%-d)-$(date +%-T).tgz

tar --create --gzip --file=$DEST_DIR$FILENAME $SRC_DIR
```

Back to [Essential Commands](../essential-commands.md)
