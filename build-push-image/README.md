# Build and Push Image

Build and push Docker Image to both Docker Hub and GitHub Container Registry (ghcr.io)

⚠️ Use all-lowercase-repository-name to prevent naming issue

## Usage

### Edge Image

```yml
- name: Checkout
  uses: actions/checkout@v2

- name: Set up Docker Meta
  id: meta
  uses: docker/metadata-action@v3
  with:
    images: |
      ${{ github.repository }}
      ghcr.io/${{ github.repository }}
    tags: |
      type=edge

- name: Build and Push Image
  uses: tomy0000000/actions/build-push-image@main
  with:
    docker_password: ${{ secrets.DOCKER_PASSWORD }}
    tags: ${{ steps.meta.outputs.tags }}
    labels: ${{ steps.meta.outputs.labels }}
```

### Latest & SemVer Image

```yml
- name: Checkout
  uses: actions/checkout@v2

- name: Set up Docker Meta
  id: meta
  uses: docker/metadata-action@v3
  with:
    images: |
      ${{ github.repository }}
      ghcr.io/${{ github.repository }}
    tags: |
      type=semver,pattern={{major}},enable=${{ !startsWith(github.ref, 'refs/tags/0.') }}
      type=semver,pattern={{major}}.{{minor}}
      type=semver,pattern={{version}}

- name: Build and Push Image
  uses: tomy0000000/actions/build-push-image@main
  with:
    docker_password: ${{ secrets.DOCKER_PASSWORD }}
    tags: ${{ steps.meta.outputs.tags }}
    labels: ${{ steps.meta.outputs.labels }}
```

## Reference

- [actions/checkout](https://github.com/actions/checkout)
- [docker/metadata-action](https://github.com/docker/metadata-action)
- [docker/setup-buildx-action](https://github.com/docker/setup-buildx-action)
- [docker/login-action](https://github.com/docker/login-action)
- [docker/build-push-action](https://github.com/docker/build-push-action)
