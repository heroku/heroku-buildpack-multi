# Heroku buildpack: multi

This buildpack has been deprecated, as the associated functionality exists natively on the Heroku platform. Please refer to https://devcenter.heroku.com/articles/buildpacks and https://devcenter.heroku.com/articles/using-multiple-buildpacks-for-an-app for documentation.

Common use cases are:

1. Running multiple language buildpacks in sequence, such as Node.js for asset preparation using NPM libraries followed by the native buildpack of your application;
1. Launching a daemon process such as [pgbouncer](https://github.com/heroku/heroku-buildpack-pgbouncer) before your application starts;
1. Pulling in system-level dependencies before the main buildpack processes your application.

## Usage

You **do not have to use this buildpack directly** on Heroku.

The `heroku buildpacks:add` command allows you to add multiple buildpacks to your application. This list of buildpacks is then properly visible through the API and command line, and you do not have to maintain a proprietary `.buildpacks` file.

For example, to have the Node.js buildpack run first, followed by the PHP buildpack (which during a build uses Node.js tools to e.g. prepare assets), run the following commands on your application:

    $ heroku buildpacks:add https://github.com/heroku/heroku-buildpack-nodejs.git
    $ heroku buildpacks:add https://github.com/heroku/heroku-buildpack-php.git

Run `heroku help buildpacks` for a full list of commands available to manage buildpacks.

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

