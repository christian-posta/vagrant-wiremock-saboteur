FROM centos:7
RUN yum install -y java-1.8.0-openjdk.x86_64 lsof wget nc tcpdump iproute initscripts unzip
RUN rpm -ivh https://github.com/tomakehurst/saboteur/releases/download/v0.7/saboteur-0.7-1.noarch.rpm
RUN service saboteur-agent start
RUN mkdir -p /home/tests && echo "tc qdisc add dev eth0 root netem delay \$1ms" > /home/tests/delay.sh && chmod +x /home/tests/delay.sh
RUN echo "tc qdisc del dev eth0 root" > /home/tests/reset.sh && chmod +x /home/tests/reset.sh
EXPOSE 8500 8888
WORKDIR /home/tests

RUN curl -s -L https://github.com/SpectoLabs/hoverfly/releases/download/v0.12.3/hoverfly_bundle_linux_386.zip -o /tmp/hoverfly.zip
RUN unzip /tmp/hoverfly.zip
ENTRYPOINT ["/home/tests/hoverfly", "-webserver"]
