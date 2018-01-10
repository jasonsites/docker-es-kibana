ARG ES_IMAGE=docker.elastic.co/elasticsearch/elasticsearch:6.0.1
FROM $ES_IMAGE

# replace default config to allow for remote reindexing
COPY --chown=elasticsearch:elasticsearch elasticsearch.yml /usr/share/elasticsearch/config/

# install the phonetic plugin (automatically available in AWS ES)
RUN bin/elasticsearch-plugin install analysis-phonetic
