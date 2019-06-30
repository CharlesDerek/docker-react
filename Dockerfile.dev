#First Temporary Build Image
FROM node:alpine as builder
#as: Specifying what stage this container container is being used for.

#WORKDIR: Specifying our working directory.
WORKDIR '/app'

#COPY: Copying over our package.json file
COPY package.json .

#RUN: Running npm install
RUN npm install

#COPY . .: Copying over all of our source code directly into the container.
COPY . .

#RUN npm build: Executing npm run build.
RUN npm run build

#notes: /app/build <--- all the stuff we care about.

#**Start Phase Below**


#Second base image
FROM nginx 

#EXPOSE: EXPOSES PORT 80 ON CONTAINER IN BEANSTALK (BACKGROUND)
EXPOSE 80

#copy over from a different building phase (identifier is 'as' tag)::
  #[ /app/build ]: The folder we want to copy over
  #[]: Where in this image (nginx) we want to place it.
    #[/usr/share...]: This path is specific use for nginx images.
COPY --from=builder /app/build /usr/share/nginx/html



#TO EXECUTE THIS IMAGE RUN THE FOLLOWING ON CLI:
 ## ~docker build .
 ## (grab {docker_id})
 ## ~docker run -p 8080:80 {docker_id}
#TO EXECUTE THIS IMAGE RUN THE PRIOR EXECUTIONS.
