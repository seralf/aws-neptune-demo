





DRAFTS
===============================================





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







