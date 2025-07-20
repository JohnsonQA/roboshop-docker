#Catalogue is a service which developed in nodejs. so get the nodejs from hub and create a workdir and copy all the 
# catalogue code and then run dependencies
#Set the env url which are dependenet on Catalogue
#Here the dns is its image name itself cuz docker automate resolve the dns.
#To run contianer we use cmd instruction and since server.js already in the opt/serer dir we can run command as below


# we not juz create an image but we have to optimize the code so that memory would be reduced and improves the performance
# For that we can go for bare minimum less memory used os which is alpine based images
# should run images with non-root user
# And also by using multi stage builds. multi stage builds are like keeping multiple dokerfiles in a single 
# dockerfile where one dockerfile is used as a builder another can use as final image. This reduces memory and 
# unnecessary installations

#============Normal way of image creation which consumes2.5GB memory ===============
# FROM node:20
# WORKDIR /opt/server
# COPY package.json .
# COPY *.js .
# RUN npm install
# ENV MONGO="true" \
#     MONGO_URL="mongodb://mongodb:27017/catalogue"
# CMD ["node", "server.js"]

#===========This reduces memory and consumes 250mb around.=============
# FROM node:20-alpine3.21
# RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
# WORKDIR /opt/server
# COPY package.json .
# COPY *.js .
# RUN npm install
# RUN chown -R roboshop:roboshop /opt/server
# ENV MONGO="true" \
#     MONGO_URL="mongodb://mongodb:27017/catalogue"
# USER roboshop
# CMD ["node","server.js"]

# Most optimized and uses 160mb for catalogue image creation by using Builder multi stage builds==========

FROM node:20-alpine3.21 AS builder
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install

FROM node:20-alpine3.21
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
WORKDIR /opt/server
USER roboshop
COPY --from=builder /opt/server /opt/server
CMD ["node","server.js"]