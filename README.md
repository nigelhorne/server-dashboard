# Monitor and visualize your web servers' health in real-time

## Introduction

This script creates a web dashboard that monitors the status of a list of web servers.
It uses the **Mojolicious** framework to build a simple web interface that shows the server status, HTTP response codes, response time, and color-coded indicators (green for healthy servers, yellow for errors like 404 or 500, and red for unreachable servers).
The list of servers to monitor is read from a file, such as `$HOME/.conf/dashboard`, and the script uses `LWP::UserAgent` to send HTTP requests and check the servers’ availability.
It also calculates the response time of each server and assigns a color to the response time, helping to quickly identify slow servers (orange for moderate delays and red for slow responses).
The dashboard auto-refreshes every 60 seconds to display up-to-date server status information.

The script also logs detailed error information into a file whenever it encounters an unreachable server or HTTP error,
recording the timestamp, the URL, the status (e.g., "Unreachable" or "HTTP Error"), and the error message (e.g., connection refusal or timeout).
The logging helps with troubleshooting by providing a history of server failures and errors.
Users can filter the dashboard to show only healthy servers or only servers with errors.
Additionally, each server URL is clickable, allowing users to directly visit the server’s webpage for more details.
This combination of real-time monitoring and logging ensures that users have both a live status overview and a historical log of issues.

To start the dashboard, run `perl bin/dashboard daemon` and connect to `http://localhost:3000`.

## **Installing Dependencies**

`apt install libhtml-treebuilder-xpath-perl libmojolicious-perl libparallel-forkmanager-perl`

### **Automatic Installation**
The dashboard relies on multiple **CPAN modules**.
If they are missing, the program will attempt to **install them automatically** when you run it for the first time **without any arguments**
and set the evironment variable BOOTSTRAP.


```
BOOTSTRAP=1 bin/dashboard
```

However, this **may fail** with a "permission denied" error if:
- You are **not running as root** (which is the correct and safer way).
- You are **not using** tools like [local::lib](https://metacpan.org/pod/local::lib) or [Perlbrew](https://perlbrew.pl/).

### **Manual Installation (If Automatic Installation Fails)**
If the modules do not install automatically, you have three options:

1. **Use `local::lib`** (Recommended)
   - Set up `local::lib` by following [these instructions](https://metacpan.org/pod/local::lib).
   - Install missing modules manually with CPAN:
     ```
     cpan install Module::Name
     ```

2. **Use Perlbrew**
   - Install [Perlbrew](https://perlbrew.pl/) to manage your Perl environment.
   - Install modules within your Perlbrew-managed environment.

3. **Run the dashboard as Root** (Not Recommended)
   - You **can** run it as root, but this **is not advised** due to security risks.

### **Alternative Installation Method (Experimental)**
You can also try installing dependencies with:

```
cpan -i lazy && perl -Mlazy bin/dashboard
```
