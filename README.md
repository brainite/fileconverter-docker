# fileconverter-docker

## Build/Test CLI

```
# Build
cd cli
docker build -t brainite/fileconverter:devel .
docker run brainite/fileconverter:devel fileconverter list extension-table

# Convert a file in the current directory
docker run -v $(pwd):/work brainite/fileconverter:devel fileconverter test.jpg test.png
```