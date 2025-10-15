# keepalived-exporter-image

Automated Docker image builds for the [gen2brain/keepalived_exporter](https://github.com/gen2brain/keepalived_exporter) Prometheus exporter.

Images are built based on daily checks on the upstream project repo. Image versions align with upstream releases (based on commit SHAs).

Keepalived must be compiled with `--enable-json` option for the exporter to work properly.

## Usage
Pull and run the latest image:

```shell
docker pull ghcr.io/jameseisele/keepalived-exporter:latest
docker run -d -p 9650:9650 ghcr.io/jameseisele/keepalived-exporter:latest
```

Or use a specific version:

```shell
docker pull ghcr.io/jameseisele/keepalived-exporter:v0.7.1
docker run -d -p 9650:9650 ghcr.io/jameseisele/keepalived-exporter:v0.7.1
```

## Architecture support
Multi-platform images supporting:
- `linux/amd64`
- `linux/arm64`

## Security
- Every built version is tracked in [versions.json](versions.json) with its corresponding commit SHA.
- If an upstream tag is rewritten (a potential compromise), the workflow will:
  - Detect the SHA mismatch.
  - Issue a security warning.
  - Halt the build automatically.
  - Require manual override with `force_rebuild=true`.
- Docker images include labels with the upstream commit SHA
- You can inspect these labels to verify what was built with:
  ```shell
  docker inspect ghcr.io/jameseisele/keepalived-exporter:v0.7.1 | jq '.[0].Config.Labels'
  ```

## License
This repository contains only build automation. The keepalived_exporter is licensed under its original license from the upstream repository.
