# Heroku buildpack: multi

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) that
allows multiple buildpacks to be used in a single deploy process. This helps support:

1. Running multiple language buildpacks such as JS for assets and Ruby for your application.
2. Running a daemon process such as [pgbouncer](https://github.com/heroku/heroku-buildpack-pgbouncer) with your application.
3. Pulling in system dependencies.

## Usage

To use this buildpack you'll first need to set it as your custom buildpack:

    $ heroku buildpacks:set https://github.com/heroku/heroku-buildpack-multi.git

From here you will need to create a `.buildpacks` file which contains (in order) the buildpacks you wish to run when you deploy:

    $ cat .buildpacks
    https://github.com/heroku/heroku-buildpack-nodejs.git#0198c71daa8
    https://github.com/heroku/heroku-buildpack-ruby.git#v86

## Writing a Multi Buildpack Compliant Buildpack

Most buildpacks install one or more system components. When using multi-buildpack it is possible to chain buildpacks together, in the previous example Node was installed and then Ruby. For this to work Ruby must have access to any environment variables needed to boot up node. For example the Node buildpack puts a node binary on the system then adds that location to the `PATH` so the system knows where to find it. If Ruby does not execute with this new `PATH`
, it won't be able to find the installed version of Node. To support this the Node buildpack writes out an `export` file that contains the necessarry exports for any other buildpack to execute Node. If you are authoring a buildpack, you should consider how other buildpacks may want to access the components you've installed and write out your own export file.

You do this by writing a to `$buildpack_dir/export` where `$buildpack_dir` is the directory the buildpack is executing in (i.e. the directory above `bin/compile`) and `export` is a text file containg bash, for example:

```
export "$PATH:\$PATH"
```

## License

MIT

## FAQ

