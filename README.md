# [cloud.iO](http://cloudio.hevs.ch/) website

This is the source code of the cloud.iO website available online at http://cloudio.hevs.ch/.

This website is based on the [SinglePaged](https://github.com/t413/SinglePaged) theme. It is powered by [Jekyll](http://jekyllrb.com) and is hosted on GitHub Pages.

## Dependencies

The website is powered by [Jekyll](https://jekyllrb.com/), a Ruby framework. The required Jekyll version is 3.1.6. You will need to install Ruby and the Ruby development kit. It's recommended to install [Bundler](https://bundler.io/) to run the website locally with ease.

## Building the site

To build the website you can use [Bundler](https://bundler.io/). First install, then clean and serve the website locally using the following commands:

```bash
$ ./script/install.sh
$ ./script/clean.sh && ./script/serve.sh
```

The generated website is available at `http://localhost:4000`.

## License

Open sourced under the [MIT license](LICENSE).