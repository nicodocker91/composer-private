Docker image for composer (with private repositories)
=====================================================

## Usage

To run composer, do:

    docker run --rm -it --volume ${COMPOSER_JSON_LOCATION}:/var/www --volume ${HOME}/.ssh:/root/.ssh --volume /etc/passwd:/etc/passwd:ro --volume /tmp/.composer-cache:/tmp/.composer nicodocker91/composer-private <composer-command>

### Right access trouble 

Running this command will make you run composer as root/super user, which is discouraged.
Nevertheless, this is mandatory when dealing with private repositories.

To go through SSH private repositories, we need to specify the volumes`${HOME}/.ssh:/root/.ssh` and `/etc/passwd:/etc/passwd:ro`.
The first one mounts your personal SSH-key so the container can access to the private network.
The second one mounts the passwords so the container can use the good one to use the SSH protocol with the given keys.

## VCS authorized

For this current version, here is the list of all authorized VCS you can use for your private repositories:

- git

## Volumes

The volumes availables to mount are `/var` and `/tmp/.composer`.
The first one is related to the workdir.
The second one is for the cache of composer.

> It is strongly encouraged to mount a local common volume dedicated to your composer cache, such as `/tmp/.composer-cache`.

The entrypoint is `/var/www`.

