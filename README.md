## Documentation

### Part 1 - Dockerize it

- Create `README.md` in main folder of your repo that details the following:
- Project Overview
- Run Project Locally
  - how you installed docker + dependencies (WSL2, for example)
    - sudo apt install docker.io
  - how to build the container
    - sudo docker build -t ff0fea8310f3:0.1 -t ff0fea8310f3:latest
  - how to run the container
    - sudo docker run --rm -it -p 8080:80 ubuntu
  - how to view the project (open a browser...go to ip and port...)
    - localhost:8080
  
### Part 2 - GitHub Actions and DockerHub  
  
- Update `README.md` in main folder of your repo to include:

- Create DockerHub public repo
  - process to create
- Allow DockerHub authentication via CLI using Dockhub credentials
- Configure GitHub Secrets
  - what credentials are needed - DockerHub credentials (do not state your credentials)
  - set secrets and secret names
- Configure GitHub Workflow
  - variables to change (repository, etc.)
  
### Part 3 - Deployment
  
- Update `README.md` in main folder of your repo to include:
- Creating a webhook
