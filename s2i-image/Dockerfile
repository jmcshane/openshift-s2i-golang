FROM openshift/base-centos7:latest

MAINTAINER jmcshane <jmcshan1@gmail.com>

EXPOSE 8080

LABEL io.k8s.description="Image for running binary applications on centos" \
      io.k8s.display-name="Go binary runner" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,go" \
      io.openshift.s2i.scripts-url=image:///usr/libexec/s2i


COPY ./s2i $STI_SCRIPTS_PATH

RUN chmod -R 777 $STI_SCRIPTS_PATH && \
    chown -R 1001:1001 $HOME

USER 1001

CMD $STI_SCRIPTS_PATH/usage
