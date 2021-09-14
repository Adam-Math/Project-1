# Project-1
The files needed for project one submission.
Setting up the ELK stack. I started a new ec2 instance using ubuntu 20.04
For the security group I chose SSH everywhere (I've had problems ssh-ing in otherwise) and TCP port 5601 
open for Kibana.

After ssh-ing into the new ec2 instance, I set up elastic search:

sudo apt-get update

sudo apt-get install default-jre

wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -

sudo apt-get install apt-transport-https

echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list

sudo apt-get update && sudo apt-get install elasticsearch

I changed items in the elasticsearch.yml file. 

Uncommenting the following:
 node.name: node-1
network.host: "localhost"
http.port: 9200
cluster.initial_master_nodes: ["node-1"]

Then started elastic search
sudo service elasticsearch start

-------------------------------------------------------------------------------
Installing Logstash

sudo apt-get install logstash

sudo service logstash start

-------------------------------------------------------------------------------
Installing Kibana
sudo apt-get install kibana

Then edit the config file.
sudo nano /etc/kibana/kibana.yml

The following items in the config file were changed or uncommented:
server.port: 5601
server.host: "0.0.0.0"
elasticsearch.hosts: ["http://localhost:9200"]

sudo service kibana start
--------------------------------------------------------------------------------
