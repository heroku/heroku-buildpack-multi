# heroku-buildpack-multi

Use multiple buildpacks on your app

Fork of https://github.com/ddollar/heroku-buildpack-multi

Compared to the original project, it expects each dependency to be in a dedicated sub
directory.

## Usage

    $ heroku config:add BUILDPACK_URL=https://github.com/ddollar/heroku-buildpack-multi.git

    $ cat .buildpacks
    subdir1=https://github.com/heroku/heroku-buildpack-nodejs.git#0198c71daa8
    subdir2=https://github.com/heroku/heroku-buildpack-ruby.git#v86


## License

MIT
