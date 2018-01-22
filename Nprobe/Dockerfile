FROM debian:latest

ADD http://apt-stable.ntop.org/jessie/all/apt-ntop-stable.deb /tmp

RUN apt-get -y update \
        && apt-get install -y lsb-release libssl-dev \
        && dpkg -i /tmp/apt-ntop-stable.deb \
        && apt-get clean all -y \
        && apt-get -y update \
        && apt-get install -y pfring nprobe ntopng ntopng-data n2disk cento \
        && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 5566 6655

RUN echo '#!/bin/bash\nnprobe "$@"' > /tmp/run.sh \
	&& chmod +x /tmp/run.sh

ENTRYPOINT ["/tmp/run.sh"]
