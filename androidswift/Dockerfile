FROM swift:4.1.3
MAINTAINER flowkey

ENV HOST_SWIFT_BIN_PATH /usr/bin

RUN apt-get update && \
    apt-get install --yes \
        xvfb lib32z1 lib32stdc++6 build-essential \
        libcurl4-openssl-dev libglu1-mesa libxi-dev libxmu-dev libglu1-mesa-dev  \
        unzip wget lsof nano vim sudo rubygems ruby-dev \
        openjdk-8-jdk

# fastlane
RUN gem install fastlane -NV

# node
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get install -y nodejs && \
    npm install -g npm@6.x.x && \
    node -v && npm -v

# android
ARG cmake_version=3.10.2.4988404
ARG sdk_version=sdk-tools-linux-3859397.zip
ARG android_home=/opt/android/sdk

RUN mkdir -p ${android_home} && \
    curl --silent --show-error --location --fail --retry 3 --output /tmp/${sdk_version} https://dl.google.com/android/repository/${sdk_version} && \
    unzip -q /tmp/${sdk_version} -d ${android_home} && \
    rm /tmp/${sdk_version}

ENV ANDROID_HOME ${android_home}
ENV PATH=${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools:${PATH}

RUN yes | sdkmanager --licenses && sdkmanager --update
RUN sdkmanager \
    "tools" \
    "platform-tools" \
    "ndk-bundle" \
    "extras;google;google_play_services" \
    "build-tools;28.0.3" \
    "platforms;android-28" \
    "cmake;${cmake_version}"

ENV PATH=${ANDROID_HOME}/cmake/${cmake_version}/bin:$PATH

# publish on dockerhub
# docker build -t flowkey/androidswift . && docker push flowkey/androidswift5