# elasticsearch 5.3 is the current version in production
FROM elasticsearch:5.3

# replace default config to allow for remote reindexing
COPY --chown=elasticsearch:elasticsearch elasticsearch.yml /usr/share/elasticsearch/config/

# install the phonetic plugin (automatically available in AWS ES)
RUN bin/elasticsearch-plugin install analysis-phonetic
