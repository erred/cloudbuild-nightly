# inspired by https://github.com/GoogleCloudPlatform/cloud-builders-community/blob/master/firebase/Dockerfile

FROM node:lts-alpine
RUN npm install -g firebase-tools
WORKDIR /workspace
ENTRYPOINT [ "firebase" ]
