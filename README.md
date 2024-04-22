I am now setting up ELK log monitoring for a nextjs app


--- setting up ELK---
**ElasticSearch** - The actual search engine powering everything, it is a reverse index engine using TF-IDF to effectively do full text search across your data

It uses Apache Lucene as the underlying search engine, but builds on top of it by creating shards and nodes to enable infinite horizontal scaling, suitable for enterprise projects.

**Logstash** - Logstash is a data processing pipeline that will be used to pipe docker logs (or any format of data) into ElasticSearch for indexing

**Kibana** - Is a UI wrapper on top of ElasticSearch that enables visualisation of data and analysis in a more intuitive way.

https://sharmarajdaksh.github.io/blog/shoving-your-docker-logs-to-elk/

The above is a great article to get started on the ELK stack using docker.

It uses the GELF (Greyhound extended log format) format to enable Docker to send its logs to logstash and subsequently ElasticSearch

Issue: When setting up ElasticSearch, you might run into this error:

Elasticsearch mount AccessDeniedException /usr/share/elasticsearch/data/nodes

To fix, run this: sudo docker exec -u 0 <containerId> chown 1000:1000 /usr/share/elasticsearch/data

This issue occurs because Elastic Search do not have certain permissions or something. So just need to change the owner of the /usr/share/elasticsearch/data folder to the user 1000 (ElasticSearch user) so that it can read and write to the datastore.


--- Setting up next-logger for proper logging format to elasticsearch---
https://github.com/vercel/next.js/discussions/54719
