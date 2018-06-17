


OUTLINE
===============================================

## Overview AWS Neptune (cos'è, come funziona) ~ 5 minuti
## Cosa sono SPARQL e Gremlin ~ 2/3 minuti
## Property Graph o RDF? ~ 2/3 minuti
## Qualche nota di introduzione a SPARQL ~ 2/3 minuti
## Qualche query di esempio SPARQL ~ 5 minuti
## Caso d'uso: Linked Data ~ 2/3 minuti
## Spiegazione dataset: http://www.dbis.informatik.uni-goettingen.de/Mondial/mondial-ER.pdf ~ 5/10 minuti
## Provare a risolvere il problema usando SQL ~ 2/3 minuti
## Provare a risolvere il problema usando SPARQL su Neptune ~ 5 minuti
## QA ~ 5 minuti



DRAFTS
===============================================

TODO: gitpitch this!




## amazon neptune SPARQL

+ presentation

	+ built from scratch 
		rumors about blazegraph team and code
	+ no bias: adopts SPARQL or gremlin

	+ possible usage
		- social networks
		- recommendations
		- fraud detection
		- network analysis
		- life sciences (bioinformatics, etc)
		- knowledge graphs
		- ML on graphs (DL and more...)
		- textual analysis (see: NLP, conceptnet/wordnet...)
		
	+ pros of neptune:
		- optimized for storage / retrieval / queries on
		- highly connected data
		- querying graphs is hard on SQL

+ features

	- based on blazegraph / acquire blazegraph team
	- SPARQL 1.1 + gremlin	
	- no support for SPARQL federated queries (security)
	- no inferencing
	- no schema concepts / constraints (SCHACL maybe?)
	- up to 64 terabytes storage, not statically allocated	
	- tested with hundred billions triples
	+ loading
		- NO load by SPARQL UPDATE da URL	
		- load by HTTP API (VPC...)
		- load by bulk load endpoint... TODO
		- NOTE: load API not ACID


+ docs amazon
	+ SPARQL API references
	https://docs.aws.amazon.com/it_it/neptune/latest/userguide/sparql-api-reference.html
	+ store etc
	https://agilevision.io/blog/aws/2018/02/26/store-and-access-graph-data-using-aws-neptune-part-1.html
	+ SPARQL HTTP API	
	https://docs.aws.amazon.com/neptune/latest/userguide/sparql-api-reference.html
	+ bulk load
	https://docs.aws.amazon.com/neptune/latest/userguide/bulk-load.html
	+ maven/java
	https://docs.aws.amazon.com/neptune/latest/userguide/access-graph-sparql-java.html

+ presentazione amazon neptune
https://www.slideshare.net/AmazonWebServices/new-launch-how-to-build-graph-applications-with-sparql-and-gremlin-using-amazon-neptune-dat342-reinvent-2017



+ video https://www.youtube.com/watch?v=6o1Ezf6NZ_E#t=26m
	- bob du charme comments on video
	http://www.snee.com/bobdc.blog/2017/12/sparql-and-amazon-web-services.html
	


----

## esempi

curl -X POST \
    -H 'Content-Type: application/json' \
    http://your-neptune-endpoint:8182/loader -d '
    { 
      "source" : "s3://neptune-us-east-1/moderngraph.ttl", 
      "format" : "turtle", 
      "accessKey" : "access-key-id", 
      "secretKey" : "secret-key", 
      "region" : "us-east-1", 
      "failOnError" : "FALSE"
    }'
SEE https://docs.aws.amazon.com/it_it/neptune/latest/userguide/access-graph-sparql.html

























* * * 


# SEE ALSO

## D3 + SPARQL visualization

https://github.com/zazuko/d3-sparql
https://github.com/bricaud/graphexp


## lectures
https://stackoverflow.com/questions/39596025/gremlin-blazegraph-remote

https://medium.com/@amolumd/graph-data-management-systems-f679b60dd9e0

https://static.googleusercontent.com/media/research.google.com/it//pubs/archive/43287.pdf
	https://github.com/facebookarchive/linkbench


## DATASETS

https://github.com/dice-group/LargeRDFBench

http://www.correlatesofwar.org/data-sets





## tate dataset 

+ neo4j
http://larkin.io/index.php/category/tate/
http://larkin.io/index.php/2015/01/05/graphing-the-tate-importing-using-neo4js-batchinserter/







