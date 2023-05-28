# AWS Route53 Failover Exercise

## Create an EC2 instance and deploy sample react application

![EC2 instance](./images/image-1.PNG)

## Deploy React application

### Install nvm on the instance

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
```

### Install nodejs
![Nodejs](./images/image-2.PNG)
```
nvm install v16.16.0
```

### Install nginx
```
sudo apt install nginx
```

### Open nginx config file which is located at the directory path
```
cd /etc/nginx && sudo nano nginx.conf
```
### Change the nginx.conf file to comment the following

![Comment the line](./images/image-3.PNG)

### Create file inside /etc/nginx/conf.d and add the following

![nginx file](./images/image-4.PNG)

![Add a record in the route53 hosted zone](./images/image-5.PNG)

### Create a S3 bucket and enable static website hosting

![Static website](./images/image-6.PNG)

### Add bucket policy for public access

```
{
    "Version": "2012-10-17",
    "Id": "PutObjPolicy",
    "Statement": [
        {
            "Sid": "DenyObjectsThatAreNotSSEKMSWithSpecificKey",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::www.ibrarmunir.co/*"
        }
    ]
}
```

### Create a health check in Route53
![Health Check](./images/image-7.PNG)

### Add failover routing policy
![Failover Routing](./images/image-8.PNG)
![Failover Routing](./images/image-9.PNG)
![Failover Routing](./images/image-10.PNG)
![Failover Routing](./images/image-11.PNG)