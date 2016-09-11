# Dev Environment Exercise

## Background
The company you work for is building a micro-service based platform. They have completed their first sprint of work and are ready to begin preparing to ship it. Being a DevOps genius, you know that it will be difficult to reproduce bugs and increase  ownership if there's not an easy way to  reliably run these services locally as you would in production. At the same time, you want to get some automation that can be reused in production.

## Your Sprint Task
Your next task is to take the two recently built Python Flask APIs and meet the following requirements:

- Read the documentation for the two Python APIs and test them to make sure they work as expected.
- Once you understand their usage, use preferred tools and technology to create automation that stands up local dev environment of the stack, including its dependency (the mongodb database). _Don't worry too much about the nuances of data storage._
- You discuss with the engineers that in order for a micro-services architecture to work best, there will need to be some http routing in front of the services so that requests go to the right places. When the stack is deployed, accessing `/api/auth` should route to the *Auth Service* while `/api/data` should point to the *Data Service*. In other words, `/api/auth/token` should access the `/token` endpoint of the auth service, etc. Use technology and tools you know to implement this behavior.

*Bonus (Optional)*
- If you haven't already, create an efficient docker image based on best practices for at least one service. Be prepared to explain why it's efficient.

## Results

Make the dev environment automation available via a public github repo with any instructions on how to run your dev environment in an accompanying `README.md` file. Send it in and be prepared to discuss it.
