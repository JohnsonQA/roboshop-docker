#We always should keep the frequently change instruction at the botton for better layer optimization. so that above 
# instructions can be re-use from cache and new layers creates for changed instructions

FROM node:20
WORKDIR /opt/server
ENV MONGO="true" \
    REDIS_URL="redis://redis:6379" \
    MONGO_URL="mongodb://mongodb:27017/users"
COPY package.json .
COPY *.js .
RUN npm install
CMD ["node", "server.js"]
