# Ansible Role GitLab Runner Autoscaling

Installs and registers a GitLab Runner with autoscaling via docker-machine

## Role Variables

### `gitlab_runner_autoscaling_docker_machine_version`: `v0.16.2`

version of docker-machine

### `gitlab_runner_autoscaling_docker_machine_driver_hetzner_version`: `3.3.0`

version of docker-machine-driver-hetzner

### `gitlab_runner_autoscaling_args`

arguments for gitlab-runner

### `gitlab_runner_autoscaling_name`: `gitlab-runner-broker`

the name of the GitLab runner

### `gitlab_runner_autoscaling_unregister`: `no`

if the GitLab runner should be unregistered

### `gitlab_runner_autoscaling_concurrent`: `5`

allowed number of concurrent GitLab runners

### `gitlab_runner_autoscaling_s3_cache_minio`: `no`

if s3 cache via [minio](https://min.io/) should be provided

### `gitlab_runner_autoscaling_s3_cache_name`: `runner`

the name of the s3 bucket shared by the GitLab runners

### `gitlab_runner_autoscaling_minio_port`: `9000`

the port minio is exposed to

### `gitlab_runner_autoscaling_minio_volume`: `/srv/minio/export`

the volume used by minio

### `gitlab_runner_autoscaling_minio_root_user`

the user name of the minio root user

### `gitlab_runner_autoscaling_minio_root_password`

the password of the minio root user

### `gitlab_runner_autoscaling_s3_cache_minio_args`

default is

```yml
  - --cache-type s3
  - --cache-s3-server-address {{ ansible_default_ipv4.address }}:{{ gitlab_runner_autoscaling_minio_port }}
  - --cache-s3-access-key {{ gitlab_runner_autoscaling_minio_root_user }}
  - --cache-s3-secret-key {{ gitlab_runner_autoscaling_minio_root_password}}
  - --cache-s3-bucket-name {{ gitlab_runner_autoscaling_s3_cache_name }}
  - --cache-s3-insecure true
```

the arguments used for registering the GitLab runner if gitlab_runner_autoscaling_s3_cache_name is yes
