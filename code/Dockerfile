FROM instructure/node:12

ENV NODE_ENV test

USER root

# Depedencies taken from here: https://github.com/puppeteer/puppeteer/blob/main/.ci/node12/Dockerfile.linux
# to allow chromium to run
RUN apt-get update --quiet=2 \
 && apt-get install --quiet=2 xvfb gconf-service libasound2 libatk1.0-0 libc6 libcairo2 libcups2 \
      libdbus-1-3 libexpat1 libfontconfig1 libgbm1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 \
      libgtk-3-0 libnspr4 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 \
      libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 \
      libxtst6 ca-certificates fonts-liberation libappindicator1 libnss3 lsb-release xdg-utils wget > /dev/null \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

USER docker

# Used to make chrome-aws-lambda run in prod mode
ENV AWS_LAMBDA_FUNCTION_NAME=screencap-lambda

COPY --chown=docker:docker ./package.json ./package-lock.json ./
RUN npm install
COPY --chown=docker:docker  . ./
