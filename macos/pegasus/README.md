# Pegasus DAS

Mass storage is managed by my Pegasus2 R4 DAS from [Promise Technology](https://www.promise.com). 

### 1. Drive Configuration

It's configured as a **RAID 5** array with the following drive loadout:

| Slot 1 | Slot 2 | Slot 3 | Slot 4 |
|---|---|---|---|
| 4 TB | 4 TB | 4 TB | 4 TB |
| Seagate | Seagate | Seagate | Seagate |
| ST4000LM024-2AN1 | ST4000DM004-2CV1 | ST4000DM004-2CV1 | ST4000DM004-2CV1 |

Once configured, the total usable space is somewhere around 12 TB total.

### 2. Driver Installation

This DAS requires drivers on macOS when in hardware RAID mode (as configured). _the "official instructions" are hosted [here](/macos/pegasus/Pegasus_DEXT_Driver_Installation_Guide_for_Sequoia.pdf)._

Do the following:

1. Install the [DEXT Driver](/macos/pegasus/Pegasus_DEXT_Driver_V21.1.0.pkg) **before** the management utility.

2. `System Settings` -> `General` -> `Login Items & Extensions` -> `Driver Extensions` -> Enable `Pegasus DEXT Driver Installer`

    2.1. Reboot macOS.

3. Install the [Promise Utility](/macos/pegasus/R_Promise_Utility_406000004.pkg) once the DAS is connected.