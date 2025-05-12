# Monitor and visualize your web servers' health in real-time

This script creates a web dashboard that monitors the status of a list of web servers.
It uses the **Mojolicious** framework to build a simple web interface that shows the server status, HTTP response codes, response time, and color-coded indicators (green for healthy servers, yellow for errors like 404 or 500, and red for unreachable servers).
The list of servers to monitor is read from a file, such as `$HOME/.conf/dashboard`, and the script uses `LWP::UserAgent` to send HTTP requests and check the servers’ availability.
It also calculates the response time of each server and assigns a color to the response time, helping to quickly identify slow servers (orange for moderate delays and red for slow responses).
The dashboard auto-refreshes every 60 seconds to display up-to-date server status information.

The script also logs detailed error information into a `server_status.log` file whenever it encounters an unreachable server or HTTP error.
It records the timestamp, the URL, the status (e.g., "Unreachable" or "HTTP Error"), and the error message (e.g., connection refusal or timeout).
The logging helps with troubleshooting by providing a history of server failures and errors.
Users can filter the dashboard to show only healthy servers or only servers with errors.
Additionally, each server URL is clickable, allowing users to directly visit the server’s webpage for more details.
This combination of real-time monitoring and logging ensures that users have both a live status overview and a historical log of issues.

To start the dashboard, run `perl bin/dashboard daemon` and connect to `http://localhost:3000`.
