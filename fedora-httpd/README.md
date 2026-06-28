# Fedora HTTPd

Build an Apache HTTPd VM image from Fedora Cloud.

### config
```ini
[build]
  tag = "my-httpd"
  base = "fedora-cloud:42"
```

### vars
```sh
DUCTTAPE="${DUCTTAPE:-$(command -v ducttape)}"
```

### build
```sh
${DUCTTAPE} build -t ${BUILD_TAG} -d ${BUILD_BASE} -f Machinefile.httpd
```

### run
```sh
${DUCTTAPE} run ${BUILD_TAG} -n ${BUILD_TAG} --publish 8080:80
```

### test
```sh
ENDPOINT=$(${DUCTTAPE} ports ${BUILD_TAG} :80)
curl http://${ENDPOINT}/ | head -n 10
```

### clean
```sh
${DUCTTAPE} stop ${BUILD_TAG}
${DUCTTAPE} rm ${BUILD_TAG}
```
