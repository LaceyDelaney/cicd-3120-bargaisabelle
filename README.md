## Documentation

### Part 1 - Dockerize it

- Project Overview 
  - This project uses Docker Hub and the docker extension on linux machines. Part 1 of the project demonstrates how
    how to download images, build and run a container, and display an html webpage on the browser. Part 2 shows how
    to create and use Github Secrets to store Docker information and recall the variables in a YAML file. Part 3
    deploys a webhook and part 4 diagrams created workflows.
- Run Project Locally
  - how you installed docker + dependencies (WSL2, for example)
    - sudo apt install docker.io
  - how to build the container
    - sudo docker build -t my-apache2 .
  - how to run the container
    - sudo docker run --rm -it -p 8080:80 ubuntu
  - how to view the project (open a browser...go to ip and port...)
    - http://localhost:8080/
    - http://127.0.0.1:8080

![curl 8080](curl8080.png)
![web 8080](web8080.png)
![port running](port8080.png)
  
### Part 2 - GitHub Actions and DockerHub  
 
- Create DockerHub public repo
  - process to create
    - access Docker Hub
    - select create repo
    - add name/description
    - select create
- Allow DockerHub authentication via CLI using Dockhub credentials
  - Access account settings and click on security
  - Create "New Access Token" and select read, write, and delete
  - Save the token in a secure location for later access
- Configure GitHub Secrets
  - what credentials are needed - DockerHub credentials (do not state your credentials)
    - open Docker Hub account settings 
    - go to Security and click on secrets to hide your username and token
  - set secrets and secret names
    - you can refer to them in a YAML file using the .secrets tag and the name of the secret
    - docker hub username (secrets.DOCKER_USERNAME)
    - docker hub token (secrets.DOCKER_TOKEN)
- Configure GitHub Workflow
  - variables to change (repository, etc.)
    - adding the Docker Hub secrets (username and password, and the image name)

```
name: docker-build-push

on: [push]

env:
  DOCKER_REPO: mysite

jobs:
  docker-build-push:
    runs-on: ubuntu-latest
    steps:
      - name: checking out repo
        uses: actions/checkout@v3
      - run: echo "post-checkout" && ls -lah && pwd
      - name: login to docker hub
        uses: docker/login-action@v1
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_TOKEN }}
      - name: docker buildx
        uses: docker/setup-buildx-action@v1
      - name: build and push
        uses: docker/build-push-action@v2
        with:
          push: true
          tags: ${{secrets.DOCKER_USERNAME }}/${{ env.DOCKER_REPO }}:latest
```
  
### Part 3 - Deployment
  
- Container restart script
  - what it does
- Webhook task definition file
  - what it does
- Setting up a webhook on the server
  - How you created you own listener
  - How you installed and are running the [webhook on GitHub](https://github.com/adnanh/webhook)
- Setting up a notifier in GitHub or DockerHub

### Part 4 - Diagramming

Include a diagram (or diagrams) of your entire workflow. Meaning it should start with a project change / update, the steps that happen in between, and end with the updated version when the server is queried (web page is accessed)
