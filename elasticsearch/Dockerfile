FROM java:8-jre
	
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.6.2.deb
sha1sum elasticsearch-5.6.2.deb 
sudo dpkg -i elasticsearch-5.6.2.deb

ENV PATH /usr/share/elasticsearch/bin:$PATH
WORKDIR /usr/share/elasticsearch
RUN set -ex \
	&& for path in \
		./data \
		./logs \
		./config \
		./config/scripts \
	; do \
		mkdir -p "$path"; \
		chown -R elasticsearch:elasticsearch "$path"; \
	done
	
COPY config ./config
COPY docker-entrypoint.sh /
EXPOSE 9200 9300

RUN chmod -R og+w /usr/share/elasticsearch
USER 1000

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["elasticsearch"]
