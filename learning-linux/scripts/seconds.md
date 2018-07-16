[CADES](http://support.cades.ornl.gov/) → [User Documentation](../../README.md) → [Linux](../linux-commands.md) → [Essential Commands](essential-commands.md) → [Script: Seconds](#)

```bash
#!/bin/bash

START=$(date +%s.%N)

# ./execute/yourprogram/here
#  Do not forget to replace your own script and uncomment the previous line by deleting #

DURATION=$(echo "$(date +%s.%N) - $START" | bc)

printf "Execution time: %.6f seconds" $DURATION
```

Back to [Essential Commands](../essential-commands.md)
