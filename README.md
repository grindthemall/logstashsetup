# logstash setup
Logstash configuration that handles Nginx logs, data being pulled from MongoDB, and data being pulled from the influxdb telegraf agent

I have posted my Logstash config file that pulls data from multiple Kafka topics for processing.  

The first set is data being sent from a MongoDB into Kafka, and is processed in one manner.
The second set is data from my Nginx front end servers.
The other sets are syslog and secure messages from all my servers
THe final set is telegraf monitoring agent data

The config file is pretty extensively commented so check that out first (lskafka.conf attached to this repo).

A few extra notes -

I do calculations on timestamp fields to check how long a given message takes to get from its originating server, into LS.
I do a second set of calculations that let me see how well my Nginx front ends, and back end application servers are performing.

There is one mutate gsub section where there are []'s around some "\".  This is intentional and required to make logstash properly process those characters, see this discussion:  https://discuss.elastic.co/t/how-to-replace-special-characters-with-a-logstash-filter/28240/2

I have added in the /usr/local/openresty/nginx/conf of this git page my nginx.conf and https.conf files that build the log messages I process with this logstash config.

# This config yields between 3.5k and 5k messages/s per 4 CPU/16GB RAM machine.
