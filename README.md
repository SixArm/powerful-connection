# powerful-connection

This macOS script determines if we have a "powerful connection".

The phrase "powerful connection" is our nickname for when our laptop
is fully powered up, and has a good wireless connection suitable for
significant networking, such as downloading big files or streaming data.


## Details

This script runs these checks:

  * The computer is running on AC power.
  * The battery is fully charged.
  * The CPU has available processing cycles.
  * The WiFi is working and is connected to a SSID.
  * The SSID accept list succeeds.
  * The SSID reject list succeeds.


## Ideas

We use this script for optionally running large network jobs.
For example, we use a daily job that checks for a powerful connection,
and if so, then the job downloads any available software updates.

We use this script as a way to check if we should run streaming.
For example, we use this script to do a check when a user signs in:
if the user has a powerful connection, then we launch video streaming.


## Exit codes

  * 0: success
  * 2x: power issue
  * 20: computer power is not plugged in
  * 21: battery power is not fully charged
  * 22: processing power is not sufficient
  * 3x: connection issue
  * 30: ssid unavailable
  * 31: ssid accept list exists, and ssid is not in it
  * 32: ssid reject list exists, and ssid is in in
  

## Configuration


Create these files:

    ~/.config/powerful-connecton/blacklist.txt
    ~/.config/powerful-connecton/whitelist.txt

Add any SSID names that you want to either list.

Add each SSID name on its own line.


## Cron

We like using the `cron` command to schedule recurring jobs.
For example, each night we check if we have powerful wifi, 
and if so, then we upgrade our system software and apps.

Example crontab lines:

    0 0 * * * powerful-connection && nice softwareupdate --install --all
    0 1 * * * powerful-connection && nice brew upgrade --cleanup
    0 2 * * * powerful-connection && nice npm update -g

Details:

  * We use the `nice` command to run the job at lower priority.

  * We use the `softwareupdate` command to update macOS.

  * We use the `brew` command to manage many of our software tools.

  * We use the `npm` command for node package management.


## References

This script is related to these repositories:

  * https://github.com/sixarm/airport-ssid
  * https://github.com/sixarm/hostinfo-commands
  * https://github.com/sixarm/pmset-commands
  * https://github.com/sixarm/ssid-powerful
  * https://github.com/sixarm/sysctl-commands
  * https://github.com/updatecommand/update


## Disclaimers

  * This script is suitable for demonstration purposes.
  * There is no warranty, express or implied.
  * Use at your own risk.
  * Your mileage may vary. 


## Tracking

  * Command: powerful-connection
  * Version: 2.0.0
  * Created: 2015-07-01
  * Updated: 2023-11-25T01:22:49Z
  * License: GPL-2.0 or GPL-3.0 or contact for custom
  * Contact: Joel Parker Henderson (joel@joelparkerhenderson.com)
