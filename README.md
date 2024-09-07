# Docker Image Trigger

## Description
This GitHub Action builds and pushes Docker images to a container registry - `ghcr.io` . It automates the process of creating Docker images based on specified inputs and metadata.

> Please note that this action is optimized to push images to GitHub Container Registry [ghcr.io](https://ghcr.io)

## Inputs

| Input Name           | Description                          | Required |
|---------------------|--------------------------------------|----------|
| `git_token`         | Git token for authentication         | Yes      |
| `release_name`      | Name of the release                  | Yes      |
| `release_version`   | Version of the release               | Yes      |
| `docker_image_vendor` | Vendor of the Docker image         | Yes      |
| `docker_context_path` | Path to the Docker context        | Yes      |

## Outputs

| Output Name | Description                     |
|-------------|---------------------------------|
| `tags`      | Docker image tags               |
| `labels`    | Docker image labels             |

## Usage

To use this action in your workflow, include the following snippet in your `.github/workflows/your-workflow.yml` file:

```yaml
- name: Build and Push Docker Image
  uses: mitch1009/docker-trigger@main
  with:
    
    git_token: ${{ secrets.GITHUN_TOKEN }}
    release_name: 'your-release-name' # Im most cased this will be the image tag
    release_version: '1.0.0' # It can be output from a version extracted from the codebase
    docker_image_vendor: 'your-org'
    docker_context_path: 'path/to/docker/context' # i.e ./
```

## Example workflow

```yaml
name: example doker build
on:
    push:
      branches:
        main
jobs:
    build:
        runs-on: ubuntu-latest
        steps:
            - name: Checkout code
              uses: actions/checkout@v4.1.7
            - name: Build and Push Docker Image
              uses: mitch1009/docker-trigger@main
              with:
                git_token: ${{ secrets.GIT_TOKEN }}
                release_name: 'your-release-name'
                release_version: 'your.version.here'
                docker_image_vendor: 'your-org-name'
                docker_context_path: 'path/to/docker/context' # i.e ./
```