# Deploy-a-High-Availability-Web-App-using-CloudFormation

## Project Requirements

### Server specs

Create a Launch Configuration for your application servers in order to deploy four servers, two located in each of your private subnets. The launch configuration will be used by an auto-scaling group.

You'll need two vCPUs and at least 4GB of RAM. The Operating System to be used is Ubuntu 18. So, choose an Instance size and Machine Image (AMI) that best fits this spec.

Be sure to allocate at least 10GB of disk space so that you don't run into issues. 

### Security Groups and Roles

Since you will be downloading the application archive from an S3 Bucket, you'll need to create an IAM Role that allows your instances to use the S3 Service.

Udagram communicates on the default HTTP Port: 80, so your servers will need this inbound port open since you will use it with the Load Balancer and the Load Balancer Health Check. As for outbound, the servers will need unrestricted internet access to be able to download and update their software.

The load balancer should allow all public traffic (0.0.0.0/0) on port 80 inbound, which is the default HTTP port. Outbound, it will only be using port 80 to reach the internal servers.

The application needs to be deployed into private subnets with a Load Balancer located in a public subnet.

One of the output exports of the CloudFormation script should be the public URL of the LoadBalancer. Add http:// in front of the load balancer DNS Name in the output

## How to run

### AWS Config
Set token: 
```
aws configure set aws_session_token <your-token>
```
Set access_id and secret_key:
```
aws configure
```
### Run yml file
```
./create.sh <cloudFormation_name> <.yaml file> <parameter.json file>
./update.sh <cloudFormation_name> <.yaml file> <parameter.json file>
```