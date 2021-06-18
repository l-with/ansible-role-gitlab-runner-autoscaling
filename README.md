# Ansible Role GitLab Runner Autoscaling
Installs and registers a GitLab Runner with autoscaling via docker-machine

## Role Variables

### `gitlab_runner_autoscaling_docker_machine_driver_hetzner_version`: `3.3.0`
version of docker-machine-driver-hetzner

### `gitlab_runner_autoscaling_args`
arguments for gitlab-runner

### `gitlab_runner_name`: `gitlab-runner-broker`
the name of the GitLab runner

### `gitlab_runner_unregister`: `no`
if the GitLab runner should be unregistered
