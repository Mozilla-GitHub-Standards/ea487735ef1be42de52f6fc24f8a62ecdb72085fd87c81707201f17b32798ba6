# Gaia Docker Taskenv

In an ideal system we could ship the exact test container environment
along with the source code that needs to run on it. With docker we can
get very very close (though limited to linux right now).

The goal here is to provide a very simple base docker image for use in
testing with the docker test host and gaia (firefox os).


# Development

## Building the docker image

You need vagrant installed already.

```sh
vagrant up
vagrant ssh
cd /vagrant
make docker_image
```

you now have a lightsofapollo/gaia-testenv container. Pass DOCKER_TAG environment variable to make to change the container tag.

## Testing

Right now the testing situation is a little messy.
From the _host_ (which needs to have node right now)

### Script unit tests

The unit tests are written in node and test the generator scripts
throughly.

```sh
make test
```

### End to end testing

The end to end tests verify everything is happy inside the docker
container.

```sh
vagrant ssh
cd /vagrant
make test-docker
```

This will do an end-to-end test inside of the vm.
