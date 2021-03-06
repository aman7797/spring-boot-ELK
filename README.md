# ELK

## PreRequest
1. Java

## ELK Configuration

![ELK Architecture](https://github.com/aman7797/spring-boot-ELK/blob/master/img/architecture.png)

### Elasticsearch

1. Download Elasticsearch from this [Elasticsearch page](https://www.elastic.co/downloads/elasticsearch) and unzip it.
2. To run the Elastic, run the below command in the command prompt
	
		bin\elasticsearch.bat
		
3. By default, it would start at 
	
		http://localhost:9200
		
   Gives the below mentioned output
	
	```json
    {
    "name" : "AMAN-LAL",
    "cluster_name" : "elasticsearch",
    "cluster_uuid" : "u1J60_ToSqW3IcZXeGz1CA",
    "version" : {
        "number" : "7.5.1",
        "build_flavor" : "default",
        "build_type" : "zip",
        "build_hash" : "3ae9ac9a93c95bd0cdc054951cf95d88e1e18d96",
        "build_date" : "2019-12-16T22:57:37.835892Z",
        "build_snapshot" : false,
        "lucene_version" : "8.3.0",
        "minimum_wire_compatibility_version" : "6.8.0",
        "minimum_index_compatibility_version" : "6.0.0-beta1"
      },
    "tagline" : "You Know, for Search"
    }
    ```
    If someone face this issue while starting from command prompt.
    
    ```swift
    
    ElasticsearchException: Failure running machine learning native code.
    ```
    Just open the **elasticsearch\config\elasticsearch.yml** and add a line
      
        xpack.ml.enabled: false

### Filebeat
1. Download Filebeat from this [Filebeat page](https://www.elastic.co/downloads/beats/filebeat) and unzip it
2. Open Filebeat.yml and change the *filebeat.inputs:* and *output*

        filebeat.inputs:
          - type: log
          # Change to true to enable this input configuration.
          enabled: true

          # Paths that should be crawled and fetched. 
          paths:
           - C:\Users\Lalpuria_am\eclipse-workspace\spring-boot-ELK\logs\*

           #----------------------------- Logstash output --------------------------------
            output.logstash:
            # The Logstash hosts
            hosts: ["localhost:5044"]
    
    For reference you can refer to [**filebeat.yml**](https://github.com/aman7797/spring-boot-ELK/blob/master/filebeat.yml)

3. Now run below command in command prompt to start Filebeat
		
		.filebeat.exe -c filebeat.yml

### Logstash

1. Download Logstash from this [Logstash page](https://www.elastic.co/downloads/logstash) and unzip it
2. Move file [**logstash.conf**](https://github.com/aman7797/spring-boot-ELK/blob/master/logstash.conf) to ..\logstash\conf
3. Now run below command in command prompt to start logstash
		
		.\bin\logstash.bat -f .\config\logstash.conf

### Kibana

1. Download Kibana from this [Kibana page](https://www.elastic.co/downloads/kibana) and unzip it
2. Open config/kibana.yml just uncomment 
  
        elasticsearch.url: "http://localhost:9200"
3. Open the command prompt on base Kibana directory and run below mentioned command

        bin\kibana.bat
4. Once started successfully, Kibana will start on default port 5601 and Kibana UI will be available at http://localhost:5601
![Kibana Homepage](https://github.com/aman7797/spring-boot-ELK/blob/master/img/kibana_start.png)


## Start with ELK

1. To create logs, run the java application and hit the endpoint

        http://localhost:8080/elk
        http://localhost:8080/exception
2. Check the logs saved in the file
3. Check the **index** in the Elasticsearch

        http://localhost:9200/_cat/indices?v
    ![Elasticsearch Index](https://github.com/aman7797/spring-boot-ELK/blob/master/img/Elasticsearch-index.png)
  
4. Go to Kibana and **Create Index**
  
    ![Kibana Create Index](https://github.com/aman7797/spring-boot-ELK/blob/master/img/create_index.png)

5. Type index name, click **Next Step** 
  
    ![Kibana Create Index Configuration](https://github.com/aman7797/spring-boot-ELK/blob/master/img/create_index_2.png)

    Select the Timestamp and done with Configuration.

6. Click on **Discover** now you can check logs in Kibana
  
    ![Kibana Logs](https://github.com/aman7797/spring-boot-ELK/blob/master/img/kibana_logs.png)