# Send logs from Logstash running on Cloud9 to S3
Follow the instructions below

1. Run the CloudFormation stack below. It will create the required resources required for this example

[![Launch CloudFormation Stack](https://sharkech-public.s3.amazonaws.com/misc-public/cloudformation-launch-stack.png)]()

The resources created by the CloudFormation stack are documented in the architecture below

</br></br></br>

2. Open the Cloud9 environment and install Logstash. Complete all of the subsequent steps in the Cloud9 terminal

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 2a. ```sudo rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 2b. ```sudo vim /etc/yum.repos.d/logstash.repo```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 2c. In the file that was created and opened in step 2b copy, paste the following for the content of the file
```
[logstash-8.x]
name=Elastic repository for 8.x packages
baseurl=https://artifacts.elastic.co/packages/8.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 2d. ```sudo yum install logstash```

3. Configure Logstash

4. Run Logstash
