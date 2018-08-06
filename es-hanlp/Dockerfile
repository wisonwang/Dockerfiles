FROM elasticsearch:5.4.3 as build

ENV ES_HOME /usr/share/elasticsearch

WORKDIR /usr/share/elasticsearch
COPY  data/elasticsearch-hanlp-5.4.3.zip . 

RUN $ES_HOME/bin/elasticsearch-plugin install x-pack
RUN $ES_HOME/bin/elasticsearch-plugin install file:///$ES_HOME/elasticsearch-hanlp-5.4.3.zip

RUN echo "-Djava.security.policy=file:///$ES_HOME/plugins/elasticsearch-hanlp/plugin-security.policy" >> config/jvm.options
RUN echo "-Djava.security.policy=file:///$ES_HOME/plugins/elasticsearch-hanlp/plugin-security.policy" >> /etc/elasticsearch/jvm.options

RUN echo 'ES_CLASSPATH="$ES_HOME/lib/*:$ES_HOME/plugins/elasticsearch-hanlp/"' >> ./bin/elasticsearch.in.sh

# RUN echo 'export ES_JAVA_OPTS="$ES_JAVA_OPTS -Djava.security.policy=file:///$ES_HOME/plugins/elasticsearch-hanlp/plugin-security.policy"' >> ./bin/elasticsearch.in.sh

ADD data hanlpdata/data

RUN chown -R elasticsearch:elasticsearch . && chmod -R 775 .

