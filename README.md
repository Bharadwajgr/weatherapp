# Weatherapp

How to run the project:

 * git clone the project in to your repository.

 * Get your openweathermap API key by signing up from the website (http://openweathermap.org/). Also, I have used Google Maps API instead of Geolocation API, but it is not possible to use it without https.Sometimes, it shows strange location. 

To run the app on the local machine:
 * Make sure that nodejs and npm are installed on your system.(Note:Use the correct versions)
 * Go to the backend folder: `npm i && APPID=<openweather-key> npm start` -> [endpoint for Helsinki] localhost:9000/api/forecast/60.192059,24.945831
 * Go to the frontend folder: `npm i && GEO_API_KEY=<googlemapsapi-key> npm start` . For instructions go [here](https://developers.google.com/maps/documentation/javascript/get-api-key) -> [For front end] localhost:8000

To run using Docker:
 * Install Docker to your system. 
 * Go to the backend folder: `docker build -t weatherapp_backend . && docker run --rm -i -p 9000:9000 -e APPID='openweather-key' --name weatherapp_backend -t weatherapp_backend`
 * Go to the frontend folder: `docker build -t weatherapp_frontend . && docker run --rm -i -p 8000:8000 -e GEO_API_KEY=<googlemapsapi-key> --name weatherapp_frontend -t weatherapp_frontend`
 (Note:-Replace the API keys in the necessary code)

To run with Docker-compose and hot reload:
  * Install Docker-compose to your system.
  * Create .env file with the content shown inside the file. (you will need openweather API and google maps API)
  * From root folder of the project run: `docker-compose up --build` and if you get an error, make sure that all your are stopped before you run the docker-compose. To stop all the running processes in docker, use the code `docker system prune`.
  * It should be running with nodemon and webpack-dev-server started to have hot reload

For the Cloud Part, check below in the Cloud Section.

There was a beautiful idea of building an app that would show the upcoming weather. The developers wrote a nice backend and a frontend following the latest principles and - to be honest - bells and whistles. However, the developers did not remember to add any information about the infrastructure or even setup instructions in the source code.

Luckily we now have [docker compose](https://docs.docker.com/compose/) saving us from installing the tools on our computer, and making sure the app looks (and is) the same in development and in production. All we need is someone to add the few missing files!

## Prerequisites

* An [openweathermap](http://openweathermap.org/) API key.

## Returning your solution

### Via github

* Make a copy of this repository in your own github account (do not fork unless you really want to be public).
* Create a personal repository in github.
* Make changes, commit them, and push them in your own repository.
* Send us the url where to find the code.

### Via tar-package

* Clone this repository.
* Make changes and **commit them**.
* Create a **.tgz** -package including the **.git**-directory, but excluding the **node_modules**-directories.
* Send us the archive.

## Exercises

Here are some things in different categories that you can do to make the app better. Before starting you need to get yourself an API key to make queries in the [openweathermap](http://openweathermap.org/). You can run the app locally using `npm i && npm start`.

### Docker

*Docker containers are central to any modern development initiative. By knowing how to set up your application into containers and make them interact with each other, you have learned a highly useful skill.*

* Add **Dockerfile**'s in the *frontend* and the *backend* directories to run them virtually on any environment having [docker](https://www.docker.com/) installed. It should work by saying e.g. `docker build -t weatherapp_backend . && docker run --rm -i -p 9000:9000 --name weatherapp_backend -t weatherapp_backend`. If it doesn't, remember to check your api key first.

* Add a **docker-compose.yml** -file connecting the frontend and the backend, enabling running the app in a connected set of containers.

* The developers are still keen to run the app and its pipeline on their own computers. Share the development files for the container by using volumes, and make sure the containers are started with a command enabling hot reload.

### Node and React development

*Node and React applications are highly popular technologies. Understanding them will give you an advantage in front- and back-end development projects.*

* The application now only reports the current weather. It should probably report the forecast e.g. a few hours from now. (tip: [openweathermap api](https://openweathermap.org/forecast5))

* There are [eslint](http://eslint.org/) errors. Sloppy coding it seems. Please help.

* The app currently reports the weather only for location defined in the *backend*. Shouldn't it check the browser location and use that as the reference for making a forecast? (tip: [geolocation](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation/Using_geolocation))

### Testing

*Test automation is key in developing good quality applications. Finding bugs in early stages of development is valuable in any software development project. With Robot Framework you can create integration tests that also serve as feature descriptions, making them exceptionally useful.*

* Create automated tests for the application. (tip: [mocha](https://mochajs.org/))

* Create [Robot Framework](http://robotframework.org/) integration tests. Hint: Start by creating a third container that gives expected weather data and direct the backend queries there by redefining the **MAP_ENDPOINT**.

### Cloud

*The biggest trend of recent times is developing, deploying and hosting your applications in cloud. Knowing cloud -related technologies is essential for modern IT specialists.*

* Set up the weather service in a free cloud hosting service, e.g. [AWS](https://aws.amazon.com/free/) or [Google Cloud](https://cloud.google.com/free/).

To run using the Google Cloud Platform, follow these steps:
  * Make sure you have an account in Google Cloud. If not you can create one. 
  * Go to APIs & Services. Check that these services are enabled: Geolocation API, Container Registry API, Kubernetes Engine API
  * Activate the cloud shell. You will find it the top right corner in the Google Cloud Console.
  * Do git clone for this repository.
  * Run this command `export APPID=<openweather-key>`
  * Run this command `export GEO_API_KEY=<googlemapsapi-key>`
  * Run using the file `./k8s_deploy.sh`
  * Wait
  * In the end you will get the addresses of frontend and backend.


To run using the AWS platform, follow these steps:
 * There are many ways of running this application on AWS. AWS has many services like DynamoDB, Elastic Beanstalk, EC2 container service or EC2 Instance. Here, I'm listing steps to run it in EC2 instance.

 * Create account on aws
 * Launch an EC2 instance
 * SSH into your instance
 * Install Node.js and npm
 * Install Git and clone repository from GitHub
 * Install Docker and Docker-compose.
 * Start the node.js app using docker-compose
 * Keep the docker-compose running

Note:-While website is working OK, for some reason, sometimes I am get an error like this - GET /sockjs-node/info?t=1562854845849 net::ERR_CONNECTION_REFUSED

### Ansible

*Automating deployment processes saves a lot of valuable time and reduces chances of costly errors. Infrastructure as Code removes manual steps and allows people to concentrate on core activities.*

* Write [ansible](http://docs.ansible.com/ansible/intro.html) playbooks for installing [docker](https://www.docker.com/) and the app itself.

### Documentation

*Good documentation benefits everyone.*

* Remember to update the README

* Use descriptive names and add comments in the code when necessary
