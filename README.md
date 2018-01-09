# Elasticsearch / Kibana / AWS Elasticsearch Service Proxy

This project creates a Docker network with 3 containers:
- Elasticsearch 5.3
- Kibana 5.3
- AWS Elasticsearch Service Proxy

It allows developers to reindex data from an ES cluster on AWS to a local environment for testing mappings, templates, queries, etc.

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
AWS_ACCESS_KEY_ID=<aws-access-key-id>
AWS_SECRET_ACCESS_KEY=<aws-secret-access-key>
DEBUG=<true || false>
REGION=<aws-region>
ENDPOINT=<aws-elasticsearch-cluster-endpoint>
```

## LICENSE
Copyright (c) 2018 Jason Sites.

Licensed under the [MIT License](LICENSE.md)
