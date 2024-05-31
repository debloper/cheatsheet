# Archive
```bash
-a, --archive    # archive (-rlptgoD)
--delete         # Delete extra files
```

# Logging
```bash
-q, --quiet
-v, --verbose
    --stats
-h, --human-readable
    --progress
-P                # same as --partial --progress
```

# Skip
```bash
-u, --update     # skip files newer on dest
-c, --checksum   # skip based on checksum, not mod-time & size
```

# Transfer
```bash
-z, --compress
-n, --dry-run
    --partial   # allows resuming of aborted syncs
```

# Xclude
```bash
--exclude=PATTERN
--include=PATTERN
```
