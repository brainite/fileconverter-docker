## Basic Usage

```
docker pull brainite/fileconverter
docker run -it --entrypoint=/bin/bash brainite/fileconverter:devel
docker run -v "$(pwd):/work" brainite/fileconverter input.jpg output.png
```

## More Information and Advanced Usage

[Visit brainite.org](https://www.brainite.org/fileconverter-docker/)