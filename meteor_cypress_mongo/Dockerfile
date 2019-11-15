FROM cypress/browsers:node10.16.0-chrome77

# install meteor
RUN curl https://install.meteor.com/ | sh
ENV METEOR_ALLOW_SUPERUSER true

# install mongo
RUN wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | apt-key add -
RUN echo "deb http://repo.mongodb.org/apt/debian stretch/mongodb-org/4.2 main" | tee /etc/apt/sources.list.d/mongodb-org-4.2.list
RUN apt-get update
RUN apt-get install -y mongodb-org

# publish on dockerhub
# docker build -t flowkey/meteor_cypress_mongo . && docker push flowkey/meteor_cypress_mongo