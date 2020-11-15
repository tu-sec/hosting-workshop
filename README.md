# Hosting Demo

This demo covers how to host a frontend application using Firebase and the Google Cloud Platform (GCP).  In it, you will see files for deploying to Firebase and also the Dockerfile that is needed to deploy to GCP's Cloud Run service.

## Requirements

You will need to download and install the following:

1. [NodeJS](https://nodejs.org/en/download/)
2. [Docker](https://docs.docker.com/get-docker/)
3. [gcloud CLI](https://cloud.google.com/sdk/docs/install)

NodeJS is 100% required for this demo.  Docker and the GCloud CLI are only required if you would like to learn how to professionally deploy your app as a docker container.  This will be the second half of the demo.

## Firebase Deployment

Steps:

1. Go to the [firebase console](https://console.firebase.google.com/) and create a new project
2. Install the firebase CLI

```
$ npm i -g firebase-tools
```

3. Log in to the firebase CLI

```
$ firebase login
```

4. Navigate to the 'sample' directory in the terminal and run the following

```
$ firebase init
```

5. After configuring the project, run the following

```
$ firebase deploy
```

## Cloud Run Deployment

Steps:

1. Create a nginx Docker file
2. Build the image (assuming in the 'sample' directory)

```
$ docker build -t gcr.io/$PROJECT_ID/client .
```

Note that the $PROJECT_ID is the ID of the google cloud platform project.  This project
is automatically created when you create a firebase application.

3. Push the new image to GCP's container registry

```
$ docker push gcr.io/$PROJECT_ID/client
```

4. Deploy the container to Cloud Run

```
$ gcloud run deploy client --image gcr.io/$PROJECT_ID/client --region us-central1 --platform managed
```