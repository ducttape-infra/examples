# Debian + Claude Code

Build, run, and share a VM image with Claude Code installed, using the
same Containerfile for both Podman/Docker and Ducttape.

### config
```ini
[build]
  tag = "debian-claude"
  base = "debian-cloud:12"

[container]
  image = "debian:12"
```

### vars
```sh
DUCTTAPE="${DUCTTAPE:-$(command -v ducttape)}"
```

### pull
```sh
${DUCTTAPE} pull ${BUILD_BASE}
```

### build
```sh
${DUCTTAPE} build -t ${BUILD_TAG} -d ${BUILD_BASE} -f Containerfile
```

### podman
```sh
podman build -t ${BUILD_TAG} -f Containerfile .
```

### run
```sh
${DUCTTAPE} run ${BUILD_TAG} -n ${BUILD_TAG} \
  -v ~/awesome-project:/workspace \
  --publish 3000:3000
```

### test
```sh
${DUCTTAPE} shell ${BUILD_TAG} "claude --version 2>/dev/null || echo 'claude not found'"
```

### clean
```sh
${DUCTTAPE} stop ${BUILD_TAG}
${DUCTTAPE} rm ${BUILD_TAG}
```
