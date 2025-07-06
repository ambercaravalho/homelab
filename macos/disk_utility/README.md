# Disk Utility RAID

Apple charges out the ass for storage upgrades at purchase time. Not only that, but the internal storage is some [proprietary BS](https://9to5mac.com/2024/11/09/m4-mac-mini-storage-upgrade/) that I don't wanna deal with at the moment.

So a couple janky USB SATA adaptors it is!

### 1. Drive Configuration

These are configured as a mirrored **RAID 1** array with the following drive loadout:

| Drive 1 | Drive 2 |
|---|---|
| 1 TB | 1 TB |
| POS Amazon Special (Source 2) | Crucial |
| MKNSSDSE1TB | CT1000MX500SSD1 |

Once configured, the total usable space is somewhere around 1 TB total _(cause it's a mirror, y'know?)_.

### 2. RAID Setup

1. `Disk Utility` -> `File` -> `RAID Assistant...`

2. `Mirrored (RAID 1)` -> select both drives -> name something cool! (`ssd_array`)

3. profit?