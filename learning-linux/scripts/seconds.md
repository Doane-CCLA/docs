
```bash
#!/bin/bash

START=$(date +%s.%N)

# ./execute/yourprogram/here
#  Do not forget to replace your own script and uncomment the previous line by deleting #

DURATION=$(echo "$(date +%s.%N) - $START" | bc)

printf "Execution time: %.6f seconds" $DURATION
```

Back to [Essential Commands](../essential-commands.md)
