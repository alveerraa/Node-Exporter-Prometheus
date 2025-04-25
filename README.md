# Node-Exporter-Prometheus

# Project Objectives

Install and run Node Exporter to collect system metrics.
Set up Prometheus and Grafana using Docker Compose.
Configure dashboards for real-time metric visualization.
Understand and troubleshoot metric collection workflows.

# 🧰 Tools & Technologies Used

Prometheus
Grafana
Node Exporter
Docker Compose
Linux/WSL/Docker

# 1. 🔧 Node Exporter Installation

✔️ Steps Followed:

Downloaded and extracted Node Exporter:
wget https://github.com/prometheus/node_exporter/releases/download/v1.9.1/node_exporter-1.9.1.linux-amd64.tar.gz
tar xvfz node_exporter-*.*-amd64.tar.gz
cd node_exporter-*.*-amd64
Ran Node Exporter:
./node_exporter
Accessible at: http://localhost:9100/metrics
Verified Output:
curl http://localhost:9100/metrics | grep "node_"
Captured WSL IP (if needed):
hostname -I

# 2. 🐳 Setup with Docker Compose

✔️ docker-compose.yml:
version: '3'
services:
  prometheus:
    image: prom/prometheus
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml

  grafana:
    image: grafana/grafana
    ports:
      - "3000:3000"
✔️ prometheus.yml:
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'node-exporter'
    static_configs:
      - targets: ['<WSL_IP>:9100']
✔️ Started Containers:
docker-compose up -d

# 3. 📊 Grafana Dashboard Setup

✔️ Accessed Grafana:
URL: http://localhost:3000
Default login: admin / admin
✔️ Added Prometheus as Data Source:
Configuration → Data Sources → Add Prometheus
URL: http://prometheus:9090
✔️ Imported Node Exporter Dashboard:
Dashboard ID: 1860
Visualizes CPU, memory, disk, and network usage.

# 💬 Observations & Learnings

Prometheus is very lightweight and easy to configure.

Grafana's plug-and-play dashboards save a lot of time.

Understanding WSL networking is crucial when mixing Windows and Linux environments.

Using docker-compose simplifies managing multiple services.
