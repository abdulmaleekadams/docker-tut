FROM node:21-alpine

# create a user with permission to run the app
# -S: createa a system user
# -G: add the user to a group
# This is done to avoid running the user as the root user
RUN addgroup app && adduser -S -G app app

# set the user to run the app
USER app

# Set working dir
WORKDIR /app

# copy package.json and it lock.json to the WD to take benefit Docker's cache
COPY package*.json ./

# to avoid EACCESS permission issue change user to root
USER root

# change the user/group ownership
RUN chown -R app:app .


# change user back to the app user
USER app

# install dep
RUN npm install

# copy the rest of files
COPY . .

# expose the port
EXPOSE 5173


# run the app
CMD ["npm", "run", "dev"]

