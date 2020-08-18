# Simple source-to-image (S2I) builder image for Apache httpd
This project was created as part of the OpenShift course. It creates a builder image so when you have a webapp that uses httpd, you can create the application on OpenShift just by using `oc new-app s2i-do288-httpd~https://github.com/user/repo` and it automatically sets up the environment and the website works.

All this app does is print "This is the index page from the app". It has no real use, and was made for learning purposes.

## Using the image
First, you have to build the builder image. 
```bash
cd s2i-do288-httpd/s2i-image
podman build -t s2i-do288-httpd . # you can also use docker, if so you will

cd ../
s2i build s2i-image/test/test-app/ s2i-do288-httpd s2i-sample-app --as-dockerfile s2i-sample-app/Dockerfile
cd s2i-sample-app
podman build --format docker -t s2i-sample-app .
podman run --name test -u 1234 -p 8080:8080 -d s2i-sample-app
curl http://localhost:8080
podman stop test
```