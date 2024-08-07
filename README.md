# Setting Up Wazuh and a Vulnerable Application with Docker

This guide will help you set up Docker containers running Wazuh and a vulnerable application (DVWA). You will also learn how to install the Wazuh agent on the vulnerable application container, perform a vulnerability scan, and configure log aggregation to the Wazuh manager.

Note: Wazuh manager: Al-amins-MacBook-Pro and Agent: DESKTOP-36G0OE5 (Home lab)
      IP: Manager: 192.168.56.1 | Agent: 192.168.32.131

# Prerequisites
Installed Docker and Docker Compose.
Local network.
Leveraged on CLI to setup wazuh

# Step 1: Deploying and integrating Wazuh with Docker
Cloned the Wazuh Docker repository:

Modified the Docker Compose file if needed:
vi to docker-compose.yml and ensure all containers(wazuh.manager, wazuh.indexer and wazuh.dashboard) are configured and pulled and match requirements.

Generated and modified certificate:
vi to generate-indexer-certs.yml and added "environment: - HTTP_PROXY=YOUR_PROXY_ADDRESS_OR_DNS"

exec cli: "docker-compose up -d" to run all wazuh containers

Verified that all containers are running: https://localhost "See attached image for UI details"

# Step 2: Setting Up the Vulnerable Application (DVWA)
Pulled the DVWA image from docker hub and ran the DVWA container, launched browser and accessed DVWA via http://localhost:8080

# Step 3: Installed and configured wazuh agent on Windows computer(DESKTOP-36G0OE5) and on the Vulnerable Application Container
Further deployed agent to the manager via the dashboard. Verified Agent host is active and being monitored, see attached images for details.
stopped agent service. 

installed the agent inside the DVWA container and configure the Wazuh agent to connect to the Wazuh manager.

modified the Wazuh agent config file located at /var/ossec/etc/ossec.conf, set  wazuh manager's IP address.

Started wazuh agent services, again verified the agent connection is active.

# Step 4: Performing a Vulnerability Scan and Configuring Log Aggregation

Perform a vulnerability scan
Note: Wazuh automatically performs vulnerability scans on connected agents, view the scan results in the Wazuh dashboard (image attached)

Configured log aggregation:
Ensured the log collection module is enabled in the Wazuh manager configuration file /var/ossec/etc/ossec.conf.
Restarted wazuh manager and checked the wazuh dashboard to ensure logs from the DVWA container are being collected and displayed.

Conclusion
Successfully set up Wazuh and a vulnerable application using Docker on local machines, and installed the Wazuh agent on the application container. Additionally, attempted to set up an AWS EC2 machine but had to terminate instances due to cost. Performed a vulnerability scan and configured log aggregation. Used the Wazuh dashboard to monitor and manage security events. Note: files and scripts were committed and pushed to GitHub, with certificates hidden for security purposes, considering the repository is public on GitHub. See attached images for details of the setup.
