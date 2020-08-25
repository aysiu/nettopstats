# nettopstats
Accumulates daily outputs of the nettop command

## What does nettopstats do?
It basically runs the `nettop` command every 15 seconds and saves the output to one .json file per day.

## How does nettopstats differ from other projects?
I'd love to be proven wrong, but at least as of the creation of nettopstats, it didn't appear that there were any projects that fit the following criteria:
- Doesn't block traffic by default (act as a firewall), forcing the user to manually approve each process using network traffic.
- Actually keeps track of accumulated traffic per process (instead of just showing the traffic per process in real time).
- Runs on macOS.

## Requirements for nettopstats
- macOS (tested on 10.15 Catalina but will likely work on other versions).
- Python 3.7 (currently points to /usr/bin/python3, but you can change that line to point to whatever location you want... may work on Python 3.8 or higher, too)
- [munkipkg](https://github.com/munki/munki-pkg) (to build the installer package) **If you're not going to use `/usr/bin/python3`, change the path in the `nettopstats` script to wherever your Python 3 is _before_ you build the pkg**

## How resource-intensive is this?
I don't know. This project may be a total failure in terms of resources. I've set it to run every 15 seconds. That's quite often, but it's also just doing a very quick dump of `nettop` output, so it may not be resource-intensive at all.

## How do you use nettopstats?
If you build and install the pkg, it should just run by itself, and then dump out daily .json files to `~/Library/Application Support/nettopstats`.

If you want to analyze the results later, run `/usr/local/bin/nettopstats --analyze daily` or `/usr/local/bin/nettopstats --analyze monthly`.

## How accurate is this tool?
Not 100% accurate, to be honest. Keep in mind, since it's running every 15 seconds and not all the time in the background, the data may be useful (just to see what processes are using the most bandwidth), but the total bytes in and total bytes out won't precisely reflect actual usage. Some bytes in and out won't be captured fully by a check that happens only every 15 seconds.

Also, standard Python (you can import special libraries) is annoying with time zones, so the by-day .json log is by whatever the time is in UTC, so you may start seeing data not exactly line up with today or yesterday, but if you just want to know roughly what's using the most bandwidth, it may not matter. Just something to keep in mind.

## What kind of support is there for nettopstats?
Right now? None. This is kind of released as is. If it works for you, great! If it doesn't, I hope you find something else. See a bug you want to fix, make a pull request, and I'll likely review it.
