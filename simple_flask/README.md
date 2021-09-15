# Simple Docker Example

[![Alt text](https://tech.4germany.org/wp-content/uploads/2020/01/Logo-Final-02-copy-1-300x109-1.png)](https://tech.4germany.org)

This example was taken from [https://medium.com/zero-equals-false/docker-introduction-what-you-need-to-know-to-start-creating-containers-8ffaf064930a](https://medium.com/zero-equals-false/docker-introduction-what-you-need-to-know-to-start-creating-containers-8ffaf064930a).

## How to execute

1. Build the docker image: `docker build -t t4g_flask_app .`
2. Start the container: `docker run --rm --name t4g_docker_example -d -p 5000:5000 t4g_flask_app`
3. Access [http://127.0.0.1:5000](http://127.0.0.1:5000) to test the app.
4. Stop the container: `docker stop t4g_docker_example`
