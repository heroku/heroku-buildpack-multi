# Heroku buildpack: multi

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) that
allows one to multiple other buildpacks in a single deploy process. This helps support:

1. Running multiple language buildpacks such as JS for assets and Ruby for your application
2. Running a daemon process such as [pgbouncer](https://github.com/heroku/heroku-buildpack-pgbouncer) with your application
3. Pulling in system dependencies.

## Usage

You **do not have to use this buildpack directly** on Heroku. Instead, the `heroku buildpacks:add` command allows you to add multiple buildpacks to your application. This list of buildpacks is then properly visible through the API and command line, and you do not have to maintain a proprietary `.buildpacks` file.

For example, to have the Node.js buildpack run first, followed by the Ruby buildpack, run the following commands on your application:

    $ heroku buildpacks:add https://github.com/heroku/heroku-buildpack-nodejs.git
    $ heroku buildpacks:add https://github.com/heroku/heroku-buildpack-ruby.git

Run `heroku help buildpacks` for a full list of commands available to manage buildpacks.

### Usage of a fork

If you have forked this buildpack to customize its behavior, you need to manually instruct Heroku to use your fork, and create a `.buildpacks` file with the list of buildpacks to run.

First, set your fork as the buildpack for your app:

    $ heroku buildpacks:set https://github.com/yourusername/heroku-buildpack-multi.git

Next, will need to create a `.buildpacks` file which contains the list of buildpacks (in the desired order) you wish to be run when you deploy:

    $ cat .buildpacks
    https://github.com/heroku/heroku-buildpack-nodejs.git
    https://github.com/heroku/heroku-buildpack-ruby.git

## License

MIT

## FAQ

