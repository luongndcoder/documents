## Kafka Install 

# Add user kafka 
- sudo adduser kafka
- sudo adduser kafka sudo
- su -l kafka

# Install Kafka
- mkdir ~/Downloads
- curl "https://downloads.apache.org/kafka/2.6.2/kafka_2.13-2.6.2.tgz" -o ~/Downloads/kafka.tgz
- mkdir ~/kafka && cd ~/kafka
- tar -xvzf ~/Downloads/kafka.tgz --strip 1

# Configuring the Kafka Server
- nano ~/kafka/config/server.properties
- add line: delete.topic.enable = true
- update line: log.dirs=/home/kafka/logs

# Creating Systemd Unit Files and Starting the Kafka Server
- sudo nano /etc/systemd/system/zookeeper.service
- make here :
    [Unit]
    Requires=network.target remote-fs.target
    After=network.target remote-fs.target

    [Service]
    Type=simple
    User=kafka
    ExecStart=/home/kafka/kafka/bin/zookeeper-server-start.sh /home/kafka/kafka/config/zookeeper.properties
    ExecStop=/home/kafka/kafka/bin/zookeeper-server-stop.sh
    Restart=on-abnormal

    [Install]
    WantedBy=multi-user.target

- sudo nano /etc/systemd/system/kafka.service
- make here :
    [Unit]
    Requires=zookeeper.service
    After=zookeeper.service

    [Service]
    Type=simple
    User=kafka
    ExecStart=/bin/sh -c '/home/kafka/kafka/bin/kafka-server-start.sh /home/kafka/kafka/config/server.properties > /home/kafka/kafka/kafka.log 2>&1'
    ExecStop=/home/kafka/kafka/bin/kafka-server-stop.sh
    Restart=on-abnormal

    [Install]
    WantedBy=multi-user.target

- sudo systemctl start kafka
- sudo systemctl status kafka
- sudo systemctl enable zookeeper
- sudo systemctl enable kafka

#  Testing the Kafka Installation
- ~/kafka/bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic TutorialTopic
- echo "Hello, World" | ~/kafka/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic TutorialTopic > /dev/null

# Hardening the Kafka Server
- sudo deluser kafka sudo
- sudo passwd kafka -l
- sudo su - kafka
- sudo passwd kafka -u