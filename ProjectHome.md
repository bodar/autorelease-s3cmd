This is a very simple project than takes N number of files and uploads them via [s3cmd](http://s3tools.org/s3cmd) using ant.

If you don't want the s3cmd dependency please use this [fork](https://code.google.com/r/songstitch-autorelease-awstasks/)

It's designed to be drop-in release build in your build pipeline. The input is a bunch of files and one property file dropped into the artifacts folder.

For example:
```
artifacts/foo-42.jar
artifacts/bar-42.jar
artifacts/release.properties
```

And release.properties contains

```
release.path=/com/example/foo
release.files=foo-42.jar,bar-42.jar
```

Server details can either be put in this file or provided as build properties for the agent

```
bucket.name=s3://some.bucket
```

Authentication is handled by s3cmd, so it's recommended that you login to the account running your build agent and setup the config file '~/.s3cfg' before running the build. Steps:

```
s3cmd --configure
```

This means that no username or password information will be visible in the log.

Then just setup your build pipeline to trigger this project