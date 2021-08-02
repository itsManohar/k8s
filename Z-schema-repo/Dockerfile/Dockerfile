FROM container-registry.alm.fkcloud.in/devkit/debian-9.13/java-jdk:8u202
ARG JARFILE
ENV user=m3-data-dapi
ENV group=m3-data
ENV UID=4089
ENV gid=4000
ENV PROJECT=schema-repo

# adding user
RUN addgroup --gid ${gid} ${group} && \
	adduser --gecos "Demo Data Claim User" --gid ${gid} -uid ${UID} --no-create-home --shell /bin/bash --disabled-login ${user}


#copy application files
COPY $JARFILE /usr/share/${PROJECT}/app.jar
RUN chown -R ${user}:${group} /usr/share/${PROJECT}

#installing base packages
RUN apt-get update && apt-get install -y \
    procps \
    net-tools \
    lsof \
    wget \
    curl
#using app user to start container
USER ${user}
#using user home to start container
WORKDIR /usr/share/${PROJECT}
CMD ["echo no default command defined ins the image"]
#timezone will be overriden when you don't set entrypoint
ENTRYPOINT ["/bin/bash", "-c"]
