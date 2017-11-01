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
  * The wifi is working.
  * The script has a list of known good SSIDs.
  * The SSID is in a list of known good SSIDs.

## Ideas

We use this script for optionally running large network jobs.
For example, we use a daily job that checks for a powerful connection,
and if so, then the job downloads any available software updates.

We use this script as a way to check if we should run streaming.
For example, we use this script to do a check when a user signs in:
if the user has a powerful connection, then we launch video streaming.

## Exit codes

  * 0: success
  * 1x: power issue
  * 10: computer power is not plugged in
  * 11: battery power is not fully charged
  * 12: processing power is not readily available
  * 2x: connection issue
  * 20: ssid unavailable
  * 21: missing list of known good ssid names
  * 22: ssid not in list of known good ssid names

## Configuration

This script uses a variable that is a list of known good SSID names.
You need to edit this list to add your favorite wifi SDD names.

If you prefer to manage the list with a data file,
then see https://github.com/sixarm/ssid-powerful

## Cron example

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
  * https://github.com/sixarm/pmset-scripts
  * https://github.com/sixarm/ssid-powerful
  * https://github.com/updatecommand/update

## Disclaimers

  * This script is suitable for demonstration purposes.
  * There is no warranty, express or implied.
  * Use at your own risk.
  * Your mileage may vary. 

## Tracking

  * Command: powerful-connection
  * Version: 1.1.1
  * Created: 2015-07-01
  * Updated: 2017-11-01
  * License: GPL
  * Contact: Joel Parker Henderson (joel@joelparkerhenderson.com)
