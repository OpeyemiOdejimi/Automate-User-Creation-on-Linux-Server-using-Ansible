# Configuring Uptime Monitoring using Gatus
Ensuring that your services and websites are available and performing as expected is crucial for maintaining user satisfaction and trust. Gatus is a simple yet powerful tool for monitoring the uptime of services and websites. This project will guide you through setting up Gatus to monitor the availability of a website or API endpoint and receive alerts when it becomes unavailable.

## Objectives
* Understand what Gatus is and its role in uptime monitoring.
* Set up Gatus on your local machine or server.
* Configure Gatus to monitor one or more endpoints.
* Set up alerting for downtime events.
* Visualize monitoring results through the Gatus dashboard.
## Prerequisites
* Basic Knowledge: Familiarity with HTTP services, APIs, and configuration files (YAML).
* Tools Required:
* A machine with Docker installed (recommended for ease of setup).
* A text editor for editing configuration files.
* Internet access for testing live endpoints.

Estimated Time
1-2 hours

## Tasks Outline
* Install and set up Gatus locally.
* Create a basic configuration file to monitor endpoints.
* Test the Gatus setup with live endpoints.
* Configure alerts for downtime using Slack, email, or another notification method.
* Explore and customize the Gatus dashboard.
## Project Tasks
**Task 1 - Install and Set Up Gatus Locally**
1. Install Docker if it’s not already installed:

* Follow the official Docker installation guide.
2. Pull the Gatus Docker image:
```
docker pull twinproduction/gatus
```
3. Create a directory for Gatus configuration:
```
mkdir gatus && cd gatus
```
4. Start Gatus using Docker with a basic setup:
```
docker run -d -p 8080:8080 --name gatus -v $(pwd)/config:/config twinproduction/gatus
```
5. Access the Gatus dashboard in your browser at http://localhost:8080.

**Task 2 - Create a Basic Configuration File**
1. Inside the gatus/config directory, create a config.yaml file.

2. Add a simple configuration to monitor a website:
```
endpoints:
  - name: Example Website
    url: "https://example.com"
    interval: 60s
    conditions:
      - "[STATUS] == 200"
```
3. Restart the Gatus container to apply the configuration:
```
docker restart gatus
```
**Task 3 - Test the Setup with Live Endpoints**
1. Add another endpoint to the config.yaml file for monitoring:
```
- name: GitHub
  url: "https://github.com"
  interval: 60s
  conditions:
    - "[STATUS] == 200"
```
2. Restart Gatus and verify the new endpoint appears on the dashboard.

3. Simulate a failure by adding a non-existent endpoint and observe the behavior:

```
- name: Nonexistent
  url: "https://thiswebsitedoesnotexist.com"
  interval: 60s
  conditions:
    - "[STATUS] == 200"
```
**Task 4 - Configure Alerts for Downtime**
1. Choose an alerting method, such as Slack or email. For example, for Slack:

* Create a Slack webhook URL in your workspace.
2. Add an alert configuration to config.yaml:
```
alerts:
  - type: slack
    url: "https://hooks.slack.com/services/YOUR/WEBHOOK/URL"
    failure-threshold: 2
    success-threshold: 2
```
3. Test the alerting by taking down a monitored service temporarily.

**Task 5 - Explore and Customize the Gatus Dashboard**
1. Access the Gatus dashboard to view uptime statistics for each endpoint.
2. Customize the dashboard appearance (e.g., themes, logos) by modifying the configuration file.
3. Adjust monitoring intervals and conditions to optimize performance.
## Conclusion
In this project, you learned how to set up and configure Gatus for monitoring uptime and performance of services and websites. You explored essential features like endpoint monitoring, alerting, and dashboard visualization. With this knowledge, you can expand your configuration to monitor multiple services, integrate with advanced alerting tools, and deploy Gatus in production environments.
