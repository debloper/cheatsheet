> [!TIP]
> `btrfs` CLI is exceptionally good at making sense, being navigated & providing contextual help.
> Still, this document stands to flatten the hierarchical discovery of subcommands "at a glance".

# FileSystem
## Review
```bash
btrfs filesystem show
btrfs filesystem usage [options] [<path>..]
```
## Inspect
```bash
btrfs filesystem df [<device>|<mount_point>]
btrfs filesystem du -s [<device>|<mount_point>]
```
## Manipulate
```bash
btrfs filesystem defragment [options] [<file>|<dir>...]
btrfs filesystem label [<device>|<mount_point>] [<newlabel>]
btrfs filesystem sync <path>
```
## Reconsider
```bash
btrfs filesystem mkswapfile <file>
btrfs filesystem resize [options] [devid:][+/-]<newsize>[kKmMgGtTpPeE]|[devid:]max <path>
```

...
