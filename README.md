# Send logs from Logstash on Cloud9 to OpenSearch

<img width="275" alt="map-user" src="https://img.shields.io/badge/cloudformation template deployments-2-blue"> <img width="85" alt="map-user" src="https://img.shields.io/badge/views-046-green"> <img width="125" alt="map-user" src="https://img.shields.io/badge/unique visits-014-green">

Follow the instructions below

1. Run the CloudFormation stack below. It will create the required resources required for this example

[![Launch CloudFormation Stack](https://sharkech-public.s3.amazonaws.com/misc-public/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=logstash-opensearch&templateURL=https://sharkech-public.s3.amazonaws.com/misc-public/logstash_cloud9_s3.yaml)

The resources created by the CloudFormation stack are documented in the architecture below

<img width="650" alt="Fluentd_cloud9_Architecture" src="https://github.com/ev2900/Logstash_Examples/blob/main/Architecture/architecture-logstash_cloud9_s3.png">

</br>

2. Open the Cloud9 environment and install Logstash. Complete all of the subsequent steps in the Cloud9 terminal

Download logstash

```curl https://artifacts.opensearch.org/logstash/logstash-oss-with-opensearch-output-plugin-7.16.2-linux-x64.tar.gz -o logstash-oss-with-opensearch-output-plugin-7.16.2-linux-x64.tar.gz```

Uncompress download

```tar -zxvf logstash-oss-with-opensearch-output-plugin-7.16.2-linux-x64.tar.gz```

3. Configure Logstash

Create configuration file

```sudo vim logstash-config.conf```

Copy / paste the following into the the ```logstash-config.conf``` file. Replace the *path*, *hosts*, *user*, *password* parts of the config

```
input {
    file {
        path => "<path_to_log_file>"
        start_position => "beginning"
    }
}
output {
    opensearch {
        hosts       => ["<opensearch_domain_endpoint>:443"]
        user        => "<opensearch_user_name>"
        password    => "<opensearch_password>"
        index       => "logstash-logs-%{+YYYY.MM.dd}"
    }
}
```
4. Run Logstash

```/home/ec2-user/environment/logstash-7.16.2/bin/logstash -f /home/ec2-user/environment/logstash-config.conf```

5. Add logs to the log file / folder specified by the path. If you need sample log data you can use the following

*Note* you made need to modify the premisions on the log file via. ```chmod 777 logstash-config.conf```

```
{"timestamp":1661869220203, "CPU": 90, "Message": "High CPU"}
{"timestamp":1661869220203, "Memory": 90, "Message": "High Memory"}
{"timestamp":1661869220203, "Disk": 80, "Message": "High Disk"}
{"timestamp":1661869220203, "Network": 100, "Message": "High Network"}
```
