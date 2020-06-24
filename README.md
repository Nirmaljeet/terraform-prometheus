
# Installation and configuration
Clone the project locally to your Docker host.

If you would like to change which targets should be monitored or make configuration changes edit the prometheus.yml file. 
The targets section is where you define what should be monitored by Prometheus(By default it monitor the EC2 instance) 

The AWS will provision and those are added as a part of variables, if you wish to change please feel free to change in variable.tf alone.

In this project we used the following provision.
* EC2 AMI - ami-0dad20bd1b9c8c004 
* EC2 Instance Type - t2.micro
* Region - Oregon
* VPC - 11.0.0.0/16
* Subnet - 11.0.1.0/24
* Port Opened - 3000, 9090

In this project the prometheus will discover the ec2 instance across the singapore region.

# Steps to run the provisioning in terraform
 Terraform initialize a working directory 
```
terraform init
```
 Terraform to create an execution plan
```
terraform plan
```
Terraform apply to provision in aws
```
terraform apply
```
Note: The above command will provision the ec2 instance and install the prometheus

# Result
```
Apply complete! Resources: 13 added, 0 changed, 0 destroyed.

Outputs:

Grafana_URL = http://54.169.85.67:3000
Prometheus_URL = http://54.169.85.67:9090
```

# Node Exporter
Now Grafana and prometheus is up and running. Now its time to run the node-exporter in the ec2 nodes which will the send the metrics to prometheus.

```
cd node-exporter
./node_exporter.sh
```

Node exporter by default send the metrics in 9100 and now you can see those metrics in prometheus and grafana(is used only for ui dashboard)

