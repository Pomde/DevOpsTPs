# The image to use to init the container, here an image with postgres to use the container as a databse
FROM postgres:14.1-alpine

# The necessary environment variables to be able to connect to the db
ENV POSTGRES_DB=tp_db \
   POSTGRES_USER=exampleuser \
   POSTGRES_PASSWORD=examplepassword

# Copy the file intializing the db to already have a db with a students table and a departments table
COPY ./docker-entrypoint-initdb.d /docker-entrypoint-initdb.d