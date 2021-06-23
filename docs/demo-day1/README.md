# DAY 1
---

## Prerequisite(s)

Please install the following application in your local device :

- install nodejs 14
- install git
- install heroku cli
- install docker and docker-compose

## CREATE GITHUB PROJECT

- #### Sign up
  - open https://github.com/join
  - fill up the registration form
  - verify your email address

- #### Create new repositories
`open repositories -> new`

- #### Open terminal and clone repository
```
$ git clone https://github.com/<user>/<repo-name>.git
```

## CREATE SIMPLE NODEJS APPLICATION

- #### Bootstrap new nodejs project
```
$ cd <repo-name>
$ npm init
```
- #### Install express
```
$ npm install express --save
```

- #### Create file index.js
```
var express = require("express");
var app = express();

app.get('/', (req, res) => {
    res.send('Simple rest api');
});

app.listen(5000, () => {
 console.log("Server running on port 5000");
});
```

- #### Add startup script
edit package.json
```
  "scripts": {
    "start": "node index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```
- #### Start application
```
$ npm start
```
- #### Open browser http://localhost:5000

- #### Create file product.json
```
[
    {
        "id": 1,
        "name": "Toyota"
    },
    {
        "id": 2,
        "name": "Mitsubishi"
    },
    {
        "id": 3,
        "name": "Chevrolet"
    }
]
```
- #### Create new function in index.js
```
var Products = require("./product.json");

//GET all list
app.get("/product/listall", (req, res) => {
    res.json(Products);
});
```
- #### Add another function in index.js
```
//GET detail by id
app.get("/product/:id", (req, res) => {
    res.json(Products.find((product) => {
        return req.params.id == product.id
    }))  
});
```
- #### Create new github token
`open profile -> settings -> developer settings -> personal access token`

- #### Authenticated to github
```
$ git remote set-url origin https://<user>:<token>@github.com/<user>/<reponame>.git
```
- #### Push changes to repository
```
$ git add -A
$ git commit -am 'initial commit'
$ git push origin main
```

## Create Heroku application

- #### Sign up
open https://signup.heroku.com/
fill up the form

- #### Create new app
open https://dashboard.heroku.com/apps
create new app (unique application name)

- #### Install Heroku CLI 
open https://devcenter.heroku.com/articles/heroku-cli

- #### login heroku cli
```
$ heroku login
```
- #### Add heroku git remote
```
$ heroku git:remote -a <app-name>
```
- #### Deploy app to Heroku
```
$ git push heroku main
```
- #### Open your heroku application in browser 
https://yourappname.herokuapp.com

`*) in this stage you will getting error in heroku app`

- #### Add this line in index.js
```
var PORT = process.env.PORT || 5000;
```
- #### Change below line in index.js
```
app.listen(5000, () => {
 console.log("Server running on port 5000");
});
```
to 
```
app.listen(PORT, () => {
 console.log("Server running on port " + PORT);
});
```
- #### Create file Procfile
```
web: node index.js
```
- #### Deploy app to Heroku
```
$ git add .
$ git commit -m 'add Procfile'
$ git push origin main
$ git push heroku main
```
- #### Re-open the app 
https://yourappname.herokuapp.com

## Setup Jenkins
- #### Clone repository
```
$ git clone https://github.com/sidiqputra/jenkins-docker.git
```
- #### Start Jenkins
```
$ cd jenkins-docker
$ docker-compose up -d
```
## Create Freestyle job to deploy application
- #### Create a job
`New Item -> Enter Job Name -> Select Freestyle project`

![Image of freestyle build env](https://github.com/sidiqputra/technoscape-demo/blob/main/docs/images/freestyle-buildenv.png?raw=true)


![Image of freestyle build script](https://github.com/sidiqputra/technoscape-demo/blob/main/docs/images/freestyle-buildscript.png?raw=true)

- #### Create new commit on the repo
- #### Trigger build
`Job -> build now`

- #### Automated build with pool scm

