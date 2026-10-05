# ECS + ECR with AWS X-Ray Sidecar

This project deploys a Flask application to Amazon ECS using AWS Fargate.

## Architecture

The application uses:

- Amazon ECR for the Flask Docker image
- Amazon ECS with AWS Fargate
- AWS X-Ray daemon as a sidecar container
- AWS Systems Manager Parameter Store
- AWS Secrets Manager
- AWS IAM task and task execution roles
- Amazon CloudWatch Logs

## Containers

### flask-app

- Flask application
- Port: 8080/TCP
- AWS X-Ray SDK enabled
- Retrieves application configuration from SSM Parameter Store
- Retrieves database password from AWS Secrets Manager

### xray-sidecar

- Image: `amazon/aws-xray-daemon`
- Port: 2000/UDP
- Sends trace information to AWS X-Ray

## AWS Resources

- ECR Repository: `tag-flask-xray-repo`
- ECS Cluster: `tag-flask-xray-cluster`
- ECS Task Definition: `tag-flask-xray-taskdef`
- ECS Service: `tag-flask-service`
- Task Role: `tag-ecs-xray-taskrole`
- Task Execution Role: `tag-ecs-xray-taskexecutionrole`
- Security Group: `tag-flask-xray-sg`
- SSM Parameter: `/tagapp/config`
- Secrets Manager Secret: `tagapp/db_password`

## Application

The Flask application runs on port 8080 and is deployed as an ECS Fargate task.

AWS X-Ray is implemented using a sidecar container to collect application traces.
