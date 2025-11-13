# RapidSpike Probe Agent

## Overview

The **RapidSpike Probe Agent** is a lightweight, containerized monitoring agent designed to perform uptime checks and network probes across multiple protocols (HTTP, TCP, ICMP, etc.) and send performance metrics back to the RapidSpike Monitoring Platform.  

It is ideal for **distributed uptime monitoring**, **internal service checks**, and **custom integration setups** where you need a self-hosted or private monitoring agent to simulate external user experience or collect localized metrics.

This image is built for **simplicity**, **observability**, and **resilience** — running silently in the background while automatically reporting errors or probe results to the RapidSpike backend.

---

## Features

- Multi-protocol probe support: **HTTP(S)**, **TCP**, **ICMP (Ping)**  
- Configurable via environment variables or mounted config file  
- Sends results securely to the RapidSpike server  
- Supports running as Docker container, VM, or lightweight image  
- Automatic retry, timeout, and silent error handling  
- Low memory footprint, fast startup time  
- Designed for isolated environments (e.g., private networks)

---

## Getting Started

1. Prerequisites

- Docker or Podman
- Optional: Vagrant/VM setup for local or isolated network monitoring
- An API key  for your RapidSpike account

<br />

2. Create Monitor and Generate API Key
- Register an account or Login into your existing [RapidSpike account](https://www.my.rapidspike.com) 
- [Generate your API Key](https://www.my.rapidspike.com)
- Set up your Probe Monitor from the dashboard

<br />

3. Pull the Image

```mermaid
docker pull rapidspike/probe-agent:latest 

```

<br />

4. Run the Container

Start the agent with minimal configuration:

```
docker run -d \
  --name rapidspike-probe \
  -e RS_AGENT_KEY="your-agent-api-key" \
  -e RS_CLIENT_ID="your-client-id" \
  rapidspike/probe-agent:latest

```
To run the agent for specific probes, pass the probe Id separated by commas. Create monitors by signing into your account on RapidSpike dashboard.

```
docker run -d \
  --name rapidspike-probe \
  -e RS_AGENT_KEY="your-agent-api-key" \
  -e RS_CLIENT_ID="your-client-id" \
  -e RS_PROBE_ID="probe-id-1,probe-id-2" \
  rapidspike/probe-agent:latest

```

<br>

4. Verify it’s Running
``` 
docker logs -f rapidspike-probe
```

<br>

Expected output:

```
[timestamp][info] Starting RapidSpike Probe Agent...
[timestamp][info] Registered probe types: HTTP, TCP, ICMP
[timestamp][info] Successfully connected to RapidSpike server

```

<br>

5. Monitor the result of your monitors from [RapidSpike dashboard](https://www.my.rapidspike.com)

<br>

### Deployment

The Probe Agent can be deployed in multiple environments including:

🐳 Docker / Kubernetes — for cloud workloads

🧱 VMs or bare-metal — for private network monitoring

☁️ AWS ECS / Fargate — for scalable regional probe clusters


### Security

- API keys are stored securely in environment variables.
- Communication between the agent and RapidSpike server is encrypted via HTTPS.
- No external ports are exposed except for internal logs and configuration.
