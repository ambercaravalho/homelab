# Colima Runtime

Docker has to run under a Linux kernel. [Colima](https://github.com/abiosoft/colima) is basically the lightest weight method of doing that on macOS.

### 1. Install Formula

1. Install Colima using Brew **first**: [brew](/macos/brew/README.md)

2. Add Login Item (run in macos terminal)

    ``` bash
    brew services colima start
    ```

### 2. Default Configuration

Copy [colima.yaml](/macos/colima/colima.yaml) from this repo to `~/.colima/default/colima.yaml` on the system.

### 3. Symbolic Link

Remember how my [internal storage space sucks](/macos/disk_utility/README.md)? Yah, this task just redirects VM disks to the `ssd_array`.

1. Stop the service:

    ``` bash
    brew services colima stop
    ```

2. Copy data from internal to external:

    ``` bash
    cp -R ~/.colima /Volumes/ssd_array/.colima
    ```

3. Remove internal folder:

    ``` bash
    rm -r ~/.colima
    ```

4. Link the folders:

    ``` bash
    ln -s /Volumes/ssd_array/.colima ~/.colima
    ```

### 4. Usage

Here are some basic commands to manage the Colima environments (or profiles as they're called).

1. Starting and stopping specific profiles:

    ``` bash
    colima start --profile colima-external_services
    colima stop --profile colima-external_services
    ```

2. Switching Docker contexts (within macOS terminal):

    ``` bash
    docker context use default
    docker context use colima-external_services
    ```

3. Directly accessing specific profiles:

    ``` bash
    colima ssh --profile colima-external_services
    exit
    ```

### 5. Troubleshooting

For some reason, colima gets stuck at “processing” in startup sequence after reboots _(but only sometimes ofc)_. Here's the fix I've found:

``` bash
rm -rf ~/.colima/_lima/_networks/user-v2
```