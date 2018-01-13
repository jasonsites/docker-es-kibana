# Development Environment for Elasticsearch / Kibana

This project creates a Docker network with 3 containers:
- Elasticsearch
- Kibana
- AWS Elasticsearch Service Proxy

It allows developers to reindex data from an ES cluster on AWS to an ES instance running in a docker environment for testing mappings, templates, queries, etc.

## Installing
Prerequisites:
- [Docker](https://www.docker.com/community-edition#/download)
- [Node 8+](https://nodejs.org)

```shell
$ git clone git@github.com:jasonsites/docker-es-kibana.git
$ cd docker-es-kibana
$ npm i
```

## Configuring
Create a `.env` file in the project root, replacing the values for each variable
```shell
# Proxy configuration
AWS_ACCESS_KEY_ID={aws-access-key-id}
AWS_SECRET_ACCESS_KEY={aws-secret-access-key}
DEBUG={true || false}
REGION={aws-region}
ENDPOINT={aws-elasticsearch-cluster-endpoint}

# Elasticsearch and Kibana images for the test environment containers
ES_IMAGE={elasticsearch-image}
KB_IMAGE={kibana-image}
```

### Elasticsearch / Kibana images:

For version 6+, use the [Elastic.co](https://www.docker.elastic.co/) dedicated registry. To avoid X-Pack configuration, append `-oss` to the end of the image *name* to use the open source version of the image.

Example using version 6.0.1:
```
ES_IMAGE=docker.elastic.co/elasticsearch/elasticsearch-oss:6.0.1
KB_IMAGE=docker.elastic.co/kibana/kibana-oss:6.0.1
```

For version 5.x, use the Docker Hub repos for [Elasticsearch](https://hub.docker.com/_/elasticsearch/) and [Kibana](https://hub.docker.com/_/kibana/).

Example using version 5.5:
```
ES_IMAGE=elasticsearch:5.5
KB_IMAGE=kibana:5.5
```

*In all cases, to avoid compatibility issues, use the same version number for the Elasticsearch and Kibana images*

### Access
The policy attached to your IAM user for accessing your AWS Elasticsearch cluster must include the "es:ESHttpGet" and "es:ESHttpPost" actions. For more information on configuring access, check out [https://aws.amazon.com/blogs/security/how-to-control-access-to-your-amazon-elasticsearch-service-domain](https://aws.amazon.com/blogs/security/how-to-control-access-to-your-amazon-elasticsearch-service-domain).

## Usage
```shell
$ docker-compose up
```
Once the environment spins up, point your browser to [http://127.0.0.1:5601](http://127.0.0.1:5601) to access the Kibana console.

To reindex data from your AWS Elasticsearch cluster to the Elasticsearch container, create an index with your mappings:
```json
PUT {test-index-name}
{
  "mappings": {
    // fill out with your mappings
  }
}
```

Then run
```json
POST _reindex
{
  "source": {
    "remote": {
      "host": "http://172.19.0.2:9210"
    },
    "index": "{aws-index-name}",
    "size": 100
  },
  "dest": {
    "index": "{test-index-name}"
  }
}
```

## LICENSE
Copyright (c) 2018 Jason Sites.

Licensed under the [MIT License](LICENSE.md)
