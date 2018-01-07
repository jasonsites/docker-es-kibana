# Elasticsearch / Kibana / AWS Elasticsearch Service Proxy

This project creates a Docker network with 3 containers:
- Elasticsearch 5.3
- Kibana 5.3
- AWS Elasticsearch Service Proxy

It allows developers to reindex data from an ES cluster on AWS to a local environment for testing mappings, templates, queries, etc.

## Installing
Prerequisites:
- [Docker](https://www.docker.com/community-edition#/download)
- [Node](https://nodejs.org)

```shell
$ git clone git@github.com:jasonsites/docker-es-kibana.git
$ cd docker-es-kibana
$ npm i
```

## Configuring
Create a `.env` file in the project root, replacing the values for each environment variable
```shell
AWS_ACCESS_KEY_ID=<aws-access-key-id>
AWS_SECRET_ACCESS_KEY=<aws-secret-access-key>
PORT=<aws-elasticsearch-proxy-port> # 9210
REGION=<aws-region> # us-west-2
ENDPOINT=<aws-elasticsearch-cluster-endpoint>
```

## Contributing
1. Clone it (`git clone git@github.com:jasonsites/docker-es-kibana.git`)
1. Create your feature branch (`git checkout -b my-new-feature`)
1. Commit your changes using [conventional changelog standards](https://github.com/bcoe/conventional-changelog-standard/blob/master/convention.md) (`git commit -am 'feat(US1234): adds my new feature'`)
1. Push to the branch (`git push origin my-new-feature`)
1. Create new Pull Request

## Releasing
1. Merge fixes & features to master
1. Run lint check `npm run lint`
1. Run security check `npm run sec`
1. Run full test suite `docker-compose run service-content-api`
1. Run release script `npm run release`
1. Push release & release tag to github `git push --follow-tags`
1. [Publish new release](https://help.github.com/articles/creating-releases/) in github, using the release notes from the [CHANGELOG](./CHANGELOG)

## LICENSE
Copyright (c) 2018 Jason Sites.

Licensed under the [MIT License](LICENSE.md)
