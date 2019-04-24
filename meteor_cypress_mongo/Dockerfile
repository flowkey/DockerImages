FROM cypress/browsers:chrome69

# install meteor
RUN curl https://install.meteor.com/ | sh

# install mongoimport
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
RUN echo "deb http://repo.mongodb.org/apt/debian jessie/mongodb-org/4.0 main" | tee /etc/apt/sources.list.d/mongodb-org-4.0.list
RUN apt-get update & wait
RUN apt-get install -y mongodb-org-tools

# publish on dockerhub
# docker build -t flowkey/meteor_cypress_mongo . && docker push flowkey/meteor_cypress_mongo