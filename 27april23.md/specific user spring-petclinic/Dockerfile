FROM alpine/git AS VCS
RUN cd / && git clone https://github.com/spring-projects/spring-petclinic.git 

FROM maven:3.9-amazoncorretto-17 AS Builder
COPY --from=VCS /spring-petclinic /spring-petclinic
RUN cd /spring-petclinic && mvn package

FROM amazoncorretto:17-alpine-jdk
LABEL author="aarkay" org="qt" project="multistage-spc"
ARG HOME_DIR=/spring-petclinic
ARG USER=dev
ARG GROUP=dev
ARG UID=1000
ARG GID=1000
RUN addgroup -g ${GID} ${GROUP} && \
adduser -h ${HOME_DIR} -u ${UID} -G ${GROUP} -D -s /bin/bash ${USER}
USER ${USER}
WORKDIR ${HOME_DIR}
COPY --from=Builder /spring-petclinic/target/spring-*.jar ${HOME_DIR}/spring-petclinc.jar
EXPOSE 8080
CMD [ "java","-jar","spring-petclinc.jar" ]