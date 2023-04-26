FROM alpine/git AS VCS
RUN cd / && git clone https://github.com/DevProjectsForDevOps/StudentCoursesRestAPI.git

FROM python:3.8-alpine
LABEL LABEL author="srikanth" org="qt" project="multistage-scr"
ARG HOME_DIR=/StudentCoursesRestAPI
ENV MYSQL_ROOT_PASSWORD=password
ENV MYSQL_USER=qtuser
ENV MYSQL_PASSWORD=srikanth
ENV MYSQL_SERVER='local host'
ENV MYSQL_PORT=3306
COPY --from=VCS /StudentCoursesRestAPI ${HOME_DIR}
WORKDIR ${HOME_DIR}
RUN pip install -r requirements.txt
EXPOSE 8080
CMD [ "python","app.py" ]