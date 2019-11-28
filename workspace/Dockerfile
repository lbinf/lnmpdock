FROM 192.168.11.200:5000/kalading/base-image/php-fpm-cli:v1

LABEL maintainer="leibinfeng <290887098@qq.com>"

# Start as root
USER root

COPY insecure_id_rsa /tmp/id_rsa
COPY insecure_id_rsa.pub /tmp/id_rsa.pub

COPY ./aliases.sh /root/aliases.sh

RUN sed -i 's/\r//' /root/aliases.sh && \
    echo "" >> ~/.bashrc && \
    echo "# Load Custom Aliases" >> ~/.bashrc && \
    echo "source ~/aliases.sh" >> ~/.bashrc && \
	echo "" >> ~/.bashrc

RUN mkdir /root/.ssh && \
	touch /root/.ssh/authorized_keys && \
    cat /tmp/id_rsa.pub >> /root/.ssh/authorized_keys && \
    cat /tmp/id_rsa.pub >> /root/.ssh/id_rsa.pub && \
    cat /tmp/id_rsa >> /root/.ssh/id_rsa && \
    rm -f /tmp/id_rsa* && \
    chmod 644 /root/.ssh/authorized_keys /root/.ssh/id_rsa.pub && \
    chmod 400 /root/.ssh/id_rsa && \
    yum install -y php71-php-ldap


# Set default work directory
WORKDIR /kalading/webroot
