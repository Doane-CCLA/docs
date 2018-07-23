
```bash
#!/bin/bash

SRC_DIR="/Users/x0y/Documents/my_work/"

DEST_DIR="/Users/x0y/Backups/"

FILENAME=Backup-$(date +%-Y%-m%-d)-$(date +%-T).tgz

tar --create --gzip --file=$DEST_DIR$FILENAME $SRC_DIR
```

Back to [Essential Commands](../essential-commands.md)
