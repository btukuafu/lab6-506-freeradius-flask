# lab6-506-freeradius-flask
This repo contains docker files to create containers for a radius server and a flask application. The flask application will then be run to be a client that authenticates into the radius server. This is a test demo
to familiarize with the radius server as well as docker containerization.

Steps to Reproduce:
1. CD into free_radius folder
2. Config radius.conf
3. Config contents of raddb directory
4. Create new image for the free_radius server by running 
the following command of the dockerfile in the free_radius directory.

cmd -> docker build -t free-radius-image .

5. Build new radius-server container with the free-radius-image

cmd -> docker run -d --name radius-server -p 5000:5000/tcp free-radius-image

6. Match configs in free_radius folder with that in flaskapp folder.
7. Create new image for the flaskapp by running the dockerfile
in the flaskapp folder using the following command.

cmd -> docker build -t flask-image .

8. Build new flaskapp container with the flask-image and 
connect it to the same network as the radius-server container.

cmd -> docker run -d --name flask-container --network container:radius-server flask-image

9. With both the radius-server container and flask-container running open up a browser
and navigate to https://localhost:5000 and enter in the credentials from your configuration
files. You should now be welcomed with a message and your username.