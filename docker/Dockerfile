FROM node:alpine as node
# targetArg is the build time argument set in docker compose. We cannot pass environment variables set in compose to dockerFile. They
# can be accessed while running the container
# ARG targetArg

# RUN echo ${targetArg}

# ENV envAtBuild ${targetArg}

# RUN echo ${envAtBuild}

ARG targetEnv

#WORKDIR /app
WORKDIR /var/${targetEnv}/docker/

COPY package.json package-lock.json ./
RUN npm cache clean --force
RUN npm install
RUN npm install pm2 -g
RUN npm install 
COPY . .
ADD /startup.sh /startup.sh
RUN chmod +x /startup.sh
ENTRYPOINT ["sh","/startup.sh"]