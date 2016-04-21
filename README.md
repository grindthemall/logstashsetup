# logstash setup
Logstash configuration that handles Nginx logs, and data being pulled from MongoDB

I have posted my Logstash config file that pulls data from two sets of Kafka topics for processing.  

The first set is data being sent from a MongoDB into Kafka, and is processed in one manner.
The second set is data from my Nginx front end servers.

The config file is pretty extensively commented so check that out first (lskafka.conf attached to this repo).

A few extra notes -

I do calculations on timestamp fields to check how long a given message takes to get from its originating server, into LS.
I do a second set of calculations that let me see how well my Nginx front ends, and back end application servers are performing.

There is one mutate gsub section where there are []'s around some "\".  This is intentional and required to make logstash properly process those characters, see this discussion:  https://discuss.elastic.co/t/how-to-replace-special-characters-with-a-logstash-filter/28240/2

Should you wish to use this Nginx setup, let me know and I will publish my full set of configs for my nginx log file setups.
