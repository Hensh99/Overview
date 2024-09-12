# Guide

### Prerequisites

1. Server with sudo access

### Steps

1. download [exporters](https://prometheus.io/download/) needed to export metrics corresponding to OS architecture.
2. extract compressed file with this command `tar xvf filename.tar.gz`
3. move folder extracted to `/usr/local/bin`
4. create user for exporter ``sudo useradd exporter --no-create-home --shell /bin/false`
5. change permission for exporter executable file `sudo chown exporter:exporter /usr/local/bin/exporter`
6. create a service file `sudo vi /etc/system/systemd/exporter.service`
7. service file like this 

```bash
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
```

1. reload the system daemon `sudo systemctl daemon-reload`
2. start exporter as a service `sudo systemctl start exporter`
3. enable exporter as a service `sudo systemctl enable exporter`
4. check server status `sudo systemctl status exporter`

# Tools

## Prometheus

Link: [Overview | Prometheus](https://prometheus.io/docs/introduction/overview/)

AWS Managed: [Infrastructure Monitoring - Amazon Managed Service for Prometheus - AWS](https://aws.amazon.com/prometheus/)

 

# Resources

[Best practices for migrating self-hosted Prometheus on Amazon EKS to Amazon Managed Service for Prometheus | AWS Open Source Blog](https://aws.amazon.com/blogs/opensource/best-practices-for-migrating-self-hosted-prometheus-on-amazon-eks-to-amazon-managed-service-for-prometheus/)

[How to install Prometheus Node Exporter on a AWS EC2 instance | by Mehmet Odabasi, PhD | Medium](https://medium.com/@mehmetodabashi/how-to-install-prometheus-node-exporter-on-a-aws-ec2-instance-ce1bf8a72160)