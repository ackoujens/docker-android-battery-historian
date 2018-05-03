# Profile Battery Usage with Batterystats and Battery Historian
## Battery Historian
### Configuration
1. [Download](https://docs.docker.com/toolbox/toolbox_install_windows/) and install Docker Toolbox (older version to be able to use on Win 7)
2. Run command in PowerShell: `docker-machine create box` to create a VM instance
3. Run command in PowerShell: `docker-machine ls` to check if instance is running
4. Run command in PowerShell: `docker-machine env box` (should display VM config and asks to run a command to config shell)
5. Run command in PowerShell: `& "C:\Program Files\Docker Toolbox\docker-machine.exe" env box | Invoke-Expression` (normally printed out in the output of previous step)
6. Run example in PowerShell: `docker run hello-world` to test configuration
7. Spin up Android Battery Historian: `docker run -p 5665:9999 gcr.io/android-battery-historian/stable:3.0 --port 9999`
8. Check the command `docker ps` to check if ports and such are configured as expected
9. Open the URL http://<DOCKERBOXIP>:5665 to navigate to Battery Historian page (tested in Chrome)

### Usage
1. Follow steps below to fetch battery statistics
2. Navigate to Battery Historian URL
3. Upload bugreport file (Convert file with NPP to UTF-8 format if an error is brought up while uploading)

## Batterystats
1. Navigate to platform-tools (folder with adb.exe)
2. Run command in PowerShell: `.\adb.exe kill-server`
3. Run command in PowerShell: `.\adb.exe devices`
4. Enable full wake history: `.\adb shell dumpsys batterystats --enable full-wake-history`
4. Run command in PowerShell: `.\adb.exe shell dumpsys batterystats --reset` (reset battery data)
5. Unplug device and perform needed battery life tests
6. Reconnect device after tests
7. Dump all battery data: `.\adb.exe shell dumpsys batterystats > [path/]batterystats.txt`
8. Create report from raw data `.\adb.exe bugreport [path/]bugreport.zip`
