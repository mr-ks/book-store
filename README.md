# Bookstore Application

This application is inspired by [istios bookinfo](https://istio.io/latest/docs/examples/bookinfo/) example app.
It is intended to demonstrate modern development practices such as microservices and containerization. The code accompanies a lecture held at TUM Heilbronn.

The main purpose of the application is to expose static information about books via a restful API.

![](docs/component.svg)

Every component is a separate Spring Boot application, which you can find in its dedicated folder. 

# Getting Started


## GitHub Actions

The repository comes with a ready to use GitHub workflow, which takes care of the continuous integration part for you.
To use it, make sure to set it up correctly:

1. Create [repository secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets) for your `DOCKER_USERNAME`
and your `DOCKER_PASSWORD`. **Do not** store sensitive information such as your username or password in the repository. Always
use an encrypted storage for that.
2. Select the bookstore component that you want to build. This can be done via the `COMPONENT` environment variable
in the [workflow file](./.github/workflows/build-push.yml)

The workflow will be triggered for every change that you do on the `main` branch. As a result of a successful workflow run
you will see a new Docker image in your personal DockerHub repository.
The naming schema is as follows:

```
${{secrets.DOCKER_USERNAME}}/bookstore-${{ env.COMPONENT }}:${{github.run_number}}
```

Every run creates a new tag to prevent cache issues while fetching the image. 
