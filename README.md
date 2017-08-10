# nova-concourse-resource

A concourse resource for use with [Nova](http://gilt-nova.readthedocs.io/en/latest/)

Makes use of the scripts from the [docker-image-resource](https://github.com/concourse/docker-image-resource) with minor modifications to support Nova.

## Example Usage

```
resource_types:
- name: nova-concourse
  privileged: true
  type: docker-image
  source:
    repository: gambtho/nova-concourse-resource
    tag: latest
    aws_access_key_id: ((aws_access_key_id))
    aws_secret_access_key: ((aws_secret_access_key))
    aws_default_region: "us-east-1"
resources:
- name: nova-runner
  type: nova-concourse
  source:
    repository: hbc-docker.jfrog.io/((app-name))
    username: ((artifactory-username))
    password: ((artifactory-password))
    aws_access_key_id: ((aws_access_key_id))
    aws_secret_access_key: ((aws_secret_access_key))
    aws_default_region: "us-east-1"
jobs: 
- put: nova-runner
  params:
    build: artifacts
    tag: artifacts/commit_sha
    tag_as_latest: true
    aws_access_key_id: ((aws_access_key_id))
    aws_secret_access_key: ((aws_secret_access_key))
    aws_default_region: "us-east-1"
    app_name: ((app-name))-repo
```
