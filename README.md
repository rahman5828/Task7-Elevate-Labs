Docker Monitoring with Netdata
Overview

This task involves setting up Netdata to monitor Docker containers, running a load test to generate activity, and verifying that the metrics are correctly displayed in the Netdata dashboard.

Steps Performed
1. Enabled Docker Monitoring in Netdata

Edited the Netdata configuration file:

/etc/netdata/go.d/docker.conf
enabled: yes
update_every: 1
autodetection_retry: 0

jobs:
  - name: local
    url: unix:///var/run/docker.sock

    Restarted Netdata service to apply changes.

2. Installed Stress Tool

Since the old progrium/stress image was deprecated, installed the stress tool inside the container environment:

apt update
apt install stress

3. Ran Load Test

Executed CPU stress test for 60 seconds with 4 CPU workers:

stress --cpu 4 --timeout 60

4. Verified Metrics in Netdata

Checked Docker Container States (running, exited, created)

Checked Docker Container Health Status (healthy, no health check, not running unhealthy)

Verified Total Docker Images and Total Image Size

Observed metric changes in real-time during stress test

Observations

Netdata successfully detected Docker containers and tracked their status.

CPU load during the stress test was reflected in the metrics.

Health status for containers without health checks was clearly shown.

Screenshots

Docker Metrics Overview


Container State and Health


Conclusion

Netdata Docker monitoring is working as expected, showing container states, health checks, and system performance metrics in real time.
