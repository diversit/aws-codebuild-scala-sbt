# Scala and sbt Dockerfile

This repository contains a **Dockerfile** for Docker, [Scala](http://www.scala-lang.org) and [sbt](http://www.scala-sbt.org).


## Based on
[AWS CodeBuild Ubuntu Java OpenJDK 8](https://github.com/aws/aws-codebuild-docker-images/blob/master/ubuntu/java/openjdk-8/Dockerfile)
But since those docker images do not seem to be publicly available, that Dockerfile has been used as the base for this Dockerfile and has been extended to install Scala and Sbt.


## Installation ##

1. Install [Docker](https://www.docker.com)
2. Pull [automated build](https://registry.hub.docker.com/u/hseeberger/scala-sbt) from public [Docker Hub Registry](https://registry.hub.docker.com):
```
docker pull diversit/aws-codebuild-scala-sbt
```
Alternatively, you can build an image from Dockerfile:
```
docker build -t diversit/aws-codebuild-scala-sbt github.com/diversit/aws-codebuild-scala-sbt
```


## Usage ##

```
docker run -it --rm diversit/aws-codebuild-scala-sbt:latest
```

Or, to reuse your local repository caches.
This also maps your current folder to the `/root/repo`
volume in the Docker container so you can build your Scala project right away.

```
docker run -it --rm -v `pwd`:/root/repo \
  -v ~/.sbt:/root/.sbt \
  -v ~/.m2:/root/.m2:rw \
  -v ~/.ivy2:/root/.ivy2:rw \
  -v ~/.coursier:/root/.coursier:rw \
  -w /root/repo \
  diversit/aws-codebuild-scala-sbt:latest
```

To build the project directly:

```
docker run -it --rm -v `pwd`:/root/repo \
  -v ~/.m2:/root/.m2:rw \
  -v ~/.ivy2:/root/.ivy2:rw \
  -v ~/.coursier:/root/.coursier:rw \
  -w /root/repo \
  diversit/aws-codebuild-scala-sbt:latest sbt clean test package
```

## Contribution policy ##

Contributions via GitHub pull requests are gladly accepted from their original author. Along with any pull requests, please state that the contribution is your original work and that you license the work to the project under the project's open source license. Whether or not you state this explicitly, by submitting any copyrighted material via pull request, email, or other means you agree to license the material under the project's open source license and warrant that you have the legal authority to do so.


## License ##

This code is open source software licensed under the [Apache 2.0 License]("http://www.apache.org/licenses/LICENSE-2.0.html").
