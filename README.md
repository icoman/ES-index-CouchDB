# Index CouchDB with Elasticsearch

A small script written in [Python](https://www.python.org/) used to index a [CouchDB](http://couchdb.apache.org/) database with [Elasticsearch](https://www.elastic.co/)  - [blog announcement](http://rainbowheart.ro/450).

![Indexing db1](http://rainbowheart.ro/static/uploads/1/2016/2/Index_ES_db1.jpg)


The python program require an ini file, created like that:

```ini

#
# Config file for indexing CouchDB with Elasticsearch
#


[ES]
index_name = db1
type_name = test1


[CouchDB]
dbname = db1
dbindex = index
index_doc_seq = db1
bulk_size = 1000


[app]
#seconds
delay = 1
verbose = True

```

Section [ES] is for Elasticsearch.
Section [CouchDB]:
dbname = which database is indexed
dbindex = in which database to store last sequence processed
index_doc_seq = name of document which keep last sequence processed
bulk_size = size of batch used to read from CouchDB and to write to ES
Section [app] keep some generic settings, after last sequence is processed, program wait for a while before to check for changes.

I used this python script to index a CouchDB database with 700 millions records:
![700 millions records CouchDB](http://rainbowheart.ro/static/uploads/1/2016/2/index_es_700_mil.jpg)
![700 millions records ES](http://rainbowheart.ro/static/uploads/1/2016/2/index_ES_benchmark_700_mil.jpg)

In case of errors (communication, LAN, memory and so on) the script restart and continue indexing:
![restart if error](http://rainbowheart.ro/static/uploads/1/2016/2/restart_index_es.jpg)

Feel free to use this software for both personal and commercial usage.

