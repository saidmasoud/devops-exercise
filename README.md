# DevOps Exercise

The code in this repo was part of a coding challenge. The implementation includes using Docker and Docker Compose to quickly and effectively set up a development environment consisting of two Python Flask APIs, a MongoDB backend, and a method to provide easy and efficient HTTP routing (NGINX was used to accomplish this).

## Prerequisutes

To implement the dev environment, install the following components:

* [Docker](https://docs.docker.com/install/)
* [Docker Compose](https://docs.docker.com/compose/install/) (some operating systems, including Windows, provide Compose as part of the Docker installation)

## Install

Installation is composed of three steps:

1. Clone the repository
`git clone https://github.com/saidmasoud/devops-exercise.git && cd devops-exercise`

2. Build the Docker images
`docker-compose build`

3. Run the containers
`docker-compose up -d`

## Discussion

When I read the problem description, I immediately know Docker+Docker Compose was going to be my solution based on my previous experience. So I first started by creating (or pulling) each individual Docker image to make sure they would properly build and run. Then I worked on creating the docker-compose.yml file to efficiently manage the entire environment.

I had some trouble with NGINX, specifically setting up the `/api/auth` and `/api/data` routes. There were two issues: 1. I had to define the Compose DNS service using the `resolver` directive, and 2. I had to add a "dummy" definition for the root route (`/`) to get the other ones to work. Once I resolved this issue, everything was working as expected. For more details, view the comments within the `nginx/nginx.conf` file.

For the "efficient Docker image" task, I designed the API Dockerfiles to first pull in the requirements.txt and run 'pip install'. That way, if a developer wanted to play around with their source code, they would not have to run 'pip install' every time they rebuilt their Docker image after a code update. This is starting to become standard practice across the Docker community, as this strategy takes advantage of the Docker caching feature which caches each step of the build.

## Original Exercise: Dev Environment

### Background
The company you work for is building a micro-service based platform. They have completed their first sprint of work and are ready to begin preparing to ship it. Being a DevOps genius, you know that it will be difficult to reproduce bugs and increase  ownership if there's not an easy way to  reliably run these services locally as you would in production. At the same time, you want to get some automation that can be reused in production.

### Your Sprint Task
Your next task is to take the two recently built Python Flask APIs and meet the following requirements:

- Read the documentation for the two Python APIs and test them to make sure they work as expected.
- Once you understand their usage, use preferred tools and technology to create automation that stands up local dev environment of the stack, including its dependency (the mongodb database). _Don't worry too much about production data storage considerations; do whatever makes the most sense for dev, we may discuss prod with you later on._
- You discuss with the engineers that in order for a micro-services architecture to work best, there will need to be some http routing in front of the services so that requests go to the right places. When the stack is deployed, accessing `/api/auth` should route to the *Auth Service* while `/api/data` should point to the *Data Service*. In other words, `/api/auth/token` should access the `/token` endpoint of the auth service, etc. Use technology and tools you know to implement this behavior.

*Bonus (Optional)*
- If you haven't already, create an efficient docker image based on best practices for at least one service. Be prepared to explain why it's efficient.

### Results

Make the dev environment automation available via a public github repo with any instructions on how to run your dev environment in an accompanying `README.md` file. Send it in and be prepared to discuss it.
