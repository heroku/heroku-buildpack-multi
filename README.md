# Heroku buildpack: multi

This buildpack has been deprecated, as the associated functionality exists natively on the Heroku platform. Please refer to https://devcenter.heroku.com/articles/buildpacks for documentation.

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

## License

MIT

## FAQ

