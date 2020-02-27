# fileconverter-docker

## Build/Test CLI

```
# Use latest version from Docker Hub
docker pull brainite/fileconverter
docker run -v $(pwd):/work brainite/fileconverter input.jpg output.png

# Develop/Build
cd {REPO_PATH}/cli
docker build -t brainite/fileconverter:devel .
docker run brainite/fileconverter:devel list extension-table
docker run -v $(pwd):/work brainite/fileconverter:devel test.jpg test.png
docker push brainite/fileconverter:devel
```