#Catalogue is a service which developed in nodejs. so get the nodejs from hub and create a workdir and copy all the 
# catalogue code and then run dependencies
#Set the env url which are dependenet on Catalogue
#Here the dns is its image name itself cuz docker automate resolve the dns.
#To run contianer we use cmd instruction and since server.js already in the opt/serer dir we can run command as below


FROM node:20
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
CMD ["node", "server.js"]
