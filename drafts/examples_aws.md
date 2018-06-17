$ history
    1  curl -X POST     -H 'Content-Type: application/json'     http://graphrm-demo.cn8ukcmczolr.eu-west-1.neptune.amazonaws.com:8182/loader
    2  curl -X POST     -H 'Content-Type: application/json'     http://graphrm-demo.cn8ukcmczolr.eu-west-1.neptune.amazonaws.com:8182/loader -d '
    3      { 
    4        "source" : "s3://neptune-seed/mondial.rdf", 
    5        "iamRoleArn" : "arn:aws:iam::400368443540:role/AWSServiceRoleForRDS ",
    6        "format" : "rdfxml", 
    7        "region" : "us-west-1", 
    8        "failOnError" : "FALSE"
    9      }'
   10  curl -X POST     -H 'Content-Type: application/json'     http://graphrm-demo.cn8ukcmczolr.eu-west-1.neptune.amazonaws.com:8182/loader -d '
   11      { 
   12        "source" : "s3://neptune-seed/mondial.rdf", 
   13        "iamRoleArn" : "arn:aws:iam::400368443540:role/AWSServiceRoleForRDS",
   14        "format" : "rdfxml", 
   15        "region" : "us-west-1", 
   16        "failOnError" : "FALSE"
   17      }'
   18  curl -X POST     -H 'Content-Type: application/json'     http://graphrm-demo.cn8ukcmczolr.eu-west-1.neptune.amazonaws.com:8182/loader -d '
   19      { 
   20        "source" : "s3://neptune-seed/mondial.rdf", 
   21        "iamRoleArn" : "arn:aws:iam::400368443540:role/AWSServiceRoleForRDS",
   22        "format" : "rdfxml", 
   23        "region" : "us-west-1", 
   24        "failOnError" : "FALSE"
   25      }'
   26  curl -X POST     -H 'Content-Type: application/json'     http://graphrm-demo.cn8ukcmczolr.eu-west-1.neptune.amazonaws.com:8182/loader -d '
   27      { 
   28        "source" : "s3://neptune-seed/mondial.rdf", 
   29        "iamRoleArn" : "arn:aws:iam::400368443540:role/NeptuneLoadFromS3",
   30        "format" : "rdfxml", 
   31        "region" : "us-west-1", 
   32        "failOnError" : "FALSE"
   33      }'
   34  curl -X POST     -H 'Content-Type: application/json'     http://graphrm-demo.cn8ukcmczolr.eu-west-1.neptune.amazonaws.com:8182/loader -d '
   35      { 
   36        "source" : "s3://neptune-seed/mondial.rdf", 
   37        "iamRoleArn" : "arn:aws:iam::400368443540:role/NeptuneLoadFromS3",
   38        "format" : "rdfxml", 
   39        "region" : "eu-west-1", 
   40        "failOnError" : "FALSE"
   41      }'
   42  curl -G 'http://graphrm-demo.cn8ukcmczolr.eu-west-1.neptune.amazonaws.com:8182/loader/3c2183be-a2bc-46dc-a10b-84b8890ef8af'
   43  curl -X POST --data-binary 'query=select ?s ?p ?o where {?s ?p ?o} limit 10' http://graphrm-demo.cn8ukcmczolr.eu-west-1.neptune.amazonaws.com:8182/sparql
   44  exit
   45  cd .ssh/authorized_keys 
   46  vim .ssh/authorized_keys 
   47  exit
   48  history
   49  exit
   50  history
