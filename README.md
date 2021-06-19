# Ansible Role GitLab Runner Autoscaling

Installs and registers a GitLab Runner with autoscaling via docker-machine and optionally a S3 cache and a docker registry proxy

## Role Variables

### `gitlab_runner_autoscaling_docker_machine_version`: `v0.16.2`

the version of docker-machine

### `gitlab_runner_autoscaling_docker_machine_driver_hetzner_version`: `3.3.0`

the version of docker-machine-driver-hetzner

### `gitlab_runner_autoscaling_args`

the arguments for gitlab-runner (except the arguments for s3 cache and registry proxy)

### `gitlab_runner_autoscaling_name`: `gitlab-runner-broker`

the name of the GitLab runner

### `gitlab_runner_autoscaling_unregister`: `no`

if the GitLab runner should be unregistered

### `gitlab_runner_autoscaling_concurrent`: `5`

the allowed number of concurrent GitLab runners

### `gitlab_runner_autoscaling_s3_cache_minio`: `no`

if s3 cache via [minio](https://min.io/) should be provided

### `gitlab_runner_autoscaling_s3_cache_name`: `runner`

the name of the s3 bucket shared by the GitLab runners

### `gitlab_runner_autoscaling_minio_address`: `"{{ ansible_default_ipv4.address }}:9000"`

the address of minio for the GitLab runners

### `gitlab_runner_autoscaling_minio_expose`: 9000

the expose for the minio container

### `gitlab_runner_autoscaling_minio_volume`: `/srv/minio/export`

the volume used by minio

### `gitlab_runner_autoscaling_minio_root_user`

the user name of the minio root user

### `gitlab_runner_autoscaling_minio_root_password`

the password of the minio root user

### `gitlab_runner_autoscaling_s3_cache_minio_args`

default is

```yml
  - --cache-shared
  - --cache-type s3
  - --cache-s3-server-address {{ gitlab_runner_autoscaling_minio_address }}
  - --cache-s3-access-key {{ gitlab_runner_autoscaling_minio_root_user }}
  - --cache-s3-secret-key {{ gitlab_runner_autoscaling_minio_root_password }}
  - --cache-s3-bucket-name {{ gitlab_runner_autoscaling_s3_cache_name }}
  - --cache-s3-insecure
```

the arguments used for registering the GitLab runner if gitlab_runner_autoscaling_s3_cache_name is yes

### `gitlab_runner_autoscaling_docker_proxy`: `no`

if docker registry cache via [registry](https://hub.docker.com/_/registry) should be provided

### `gitlab_runner_autoscaling_docker_proxy_address`: `"{{ ansible_default_ipv4.address }}:5000"`

the address of the docker registry proxy for the GitLab runners

### `gitlab_runner_autoscaling_docker_proxy_url`: `"http://{{ gitlab_runner_autoscaling_docker_proxy_address }}"`

the url of the docker registry proxy for the GitLab runners

### `gitlab_runner_autoscaling_docker_proxy_expose`: `5000`

the expose for the registry container

### `gitlab_runner_autoscaling_docker_proxy_remote_url`: `https://registry-1.docker.io`

the value for `REGISTRY_PROXY_REMOTEURL` for the registry container

### `gitlab_runner_autoscaling_docker_proxy_args`

default is

```yml
  - --machine-machine-options "engine-registry-mirror={{ gitlab_runner_autoscaling_docker_proxy_url }}"
  - --machine-machine-options "engine-insecure-registry={{ gitlab_runner_autoscaling_docker_proxy_address }}"
```
