# Elastic Search 

Elasticsearch is a search engine based on the Lucene (Apache) library. It provides a distributed, multitenant-capable full-text search engine with an HTTP web interface and schema-free JSON documents.

# Elastic Stack (ELT Stack)
<img width="583" alt="Screenshot 2022-07-18 at 6 46 34 AM" src="https://user-images.githubusercontent.com/3948750/179433053-ec42a3eb-cb23-437d-b0e4-41d019422c17.png">

# Kibana 

Create dashboard, 

## How start 

```cmd
ssh <ssh url>
systemctl status kibana // to check the status
```

## How it will work 

Please follow the below steps 

1. Create Bucket - Index go to 'Dev Tool'. Add index name e.g: `GET userList` click run. To check the index added, go to Stack management -> Index patterns 
2. How to Put data inside the bucket - index  
  - API `curl -XPOST http://elasticnode/<indexName>/<_doc or _create>/ -H 'Content-Type: application/json' -d '{ "@timestamp": '', users: [] }' `
  - Upload JSON in Kibana 
  - Beats & Logstash
