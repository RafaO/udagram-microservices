# Udagram Image Filtering Microservice

Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.

The project is split into three parts:
1. [The Simple Frontend](/udacity-c3-frontend)
A basic Ionic client web application which consumes the RestAPI Backend. 
2. [The RestAPI Feed Backend](/udacity-c3-restapi-feed), a Node-Express feed microservice.
3. [The RestAPI User Backend](/udacity-c3-restapi-user), a Node-Express user microservice.

## Getting Setup

> _tip_: this frontend is designed to work with the RestAPI backends). It is recommended you stand up the backend first, test using Postman, and then the frontend should integrate.

### Installing Node and NPM
This project depends on Nodejs and Node Package Manager (NPM). Before continuing, you must download and install Node (NPM is included) from [https://nodejs.com/en/download](https://nodejs.org/en/download/).

### Installing Ionic Cli
The Ionic Command Line Interface is required to serve and build the frontend. Instructions for installing the CLI can be found in the [Ionic Framework Docs](https://ionicframework.com/docs/installation/cli).

### Installing project dependencies

This project uses NPM to manage software dependencies. NPM Relies on the package.json file located in the root of this repository. After cloning, open your terminal and run:
```bash
npm install
```
>_tip_: **npm i** is shorthand for **npm install**

### Setup Backend Node Environment
You'll need to create a new node server. Open a new terminal within the project directory and run:
1. Initialize a new project: `npm init`
2. Install express: `npm i express --save`
3. Install typescript dependencies: `npm i ts-node-dev tslint typescript  @types/bluebird @types/express @types/node --save-dev`
4. Look at the `package.json` file from the RestAPI repo and copy the `scripts` block into the auto-generated `package.json` in this project. This will allow you to use shorthand commands like `npm run dev`


### Configure The Backend Endpoint
Ionic uses enviornment files located in `./src/enviornments/enviornment.*.ts` to load configuration variables at runtime. By default `environment.ts` is used for development and `enviornment.prod.ts` is used for produciton. The `apiHost` variable should be set to your server url either locally or in the cloud.

***
### Running the Development Server
Ionic CLI provides an easy to use development server to run and autoreload the frontend. This allows you to make quick changes and see them in real time in your browser. To run the development server, open terminal and run:

```bash
ionic serve
```

### Building the Static Frontend Files
Ionic CLI can build the frontend into static HTML/CSS/JavaScript files. These files can be uploaded to a host to be consumed by users on the web. Build artifacts are located in `./www`. To build from source, open terminal and run:
```bash
ionic build
```
***

## Submission information

### Docker hub images:
* https://hub.docker.com/repository/docker/rafao/udagram-frontend
* https://hub.docker.com/repository/docker/rafao/udagram-backend-user
* https://hub.docker.com/repository/docker/rafao/simple-reverse-proxy
* https://hub.docker.com/repository/docker/rafao/udagram-backend-feed

### Running the project:
In order to run the project locally, you would need to update your secrets in your environment variables and the configuration files. Then, deploy to kubernetes with the following comand:
```bash
$> kubectl apply -f udacity-c3-deployment/k8s/
```
After that, verify that your pods are running with
```bash
$> kubectl get pods
```
Forward the ports to be able to find reverse proxy and frontend services:
```bash
$> kubectl port-forward service/frontend 8100:8100
$> kubectl port-forward service/reverseproxy 8080:8080
```
Open your favorite browser and go to `localhost:8100`

### CD
Once you have your cluster configured, you need to uncomment the last line in `travis.yml` file to deploy the app in every CI iteration.

### Screenshots
You can find screenshots of the running pods, app, and travis under the [screenshots](https://github.com/RafaO/udagram-microservices/blob/master/screenshots) directory.
