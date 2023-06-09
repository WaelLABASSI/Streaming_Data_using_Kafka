# Streaming_Data_using_Kafka

This project aims to de-congest the national highways by analyzing the road traffic data from different toll plazas. As a vehicle passes a toll plaza, the vehicle's data like vehicle_id, vehicle_type, toll_plaza_id and timestamps are stremed to Kafka.

1. Set MySQL database and Prepare the project environment
    - Start a MySQL Database server
    - Create a table to hold the toll data that will be generated by the traffic simulator (kafka)
    
      create database tolldata;
      use tolldata;
      create table livetolldata(timestamp datetime,vehicle_id int,vehicle_type char(15),toll_plaza_id smallint);
    
    - Install the MySQL python driver to interract with the database
    
      pip3 install mysql-connector-python 
    
    - Install the Kafka python driver to communicate with kafka server
    
      pip3 install kafka-python
    
    
2. Download and extract Kafka
    - Start zookeeper server
      bin/zookeeper-server-start.sh config/zookeeper.properties
      
    - Start Kafka server in a new terminal
      bin/kafka-server-start.sh config/server.properties
    
3. Create the streaming pipeline in a new terminal
    - Create a topic named toll in Kafka
      bin/kafka-topics.sh --create --topic toll -bootstrap-server localhost:9092 --replication-factor 1 --partitions 1
      
    - Run toll_traffic_generator.py to stream generated data to toll topic
    
    - Configure streaming_data_reader.py in order to connect to the mysql server (set the parameters: TOPIC, DATABASE, USERNAME and PASSWORD)
    - Run streaming_data_reader.py to write streamed data into the MySQL database table livetolldata
    
    - Streaming data will be collected in the database table
    
    
    
## Credits
IBM Coursera Course: ETL and Data Pipelines with SHELL, Airflow and Kafka
