###########
# BUILDER #
###########

# pull base image
FROM python:3.8

# set work directory
WORKDIR /usr/src/app

# install system dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends gcc

    # install python dependencies
COPY ./requirements.txt .

# create directory for the app user
RUN mkdir -p /home/app

# create the app user
RUN addgroup --system app && adduser --system --group app

# create the appropriate directories
ENV HOME=/home/app
ENV APP_HOME=/home/app/web
RUN mkdir $APP_HOME
WORKDIR $APP_HOME


# copy entrypoint-prod.sh
COPY ./entrypoint.sh $APP_HOME

# copy project
COPY . $APP_HOME

# chown all the files to the app user
RUN chown -R app:app $APP_HOME

# change to the app user
USER app

# run entrypoint.prod.sh
ENTRYPOINT ["/home/app/web/entrypoint.sh"]