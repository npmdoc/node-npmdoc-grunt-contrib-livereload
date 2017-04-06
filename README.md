# api documentation for  [grunt-contrib-livereload (v0.1.2)](https://github.com/gruntjs/grunt-contrib-livereload)  [![npm package](https://img.shields.io/npm/v/npmdoc-grunt-contrib-livereload.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-grunt-contrib-livereload) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-grunt-contrib-livereload.svg)](https://travis-ci.org/npmdoc/node-npmdoc-grunt-contrib-livereload)
#### Reload assets live in the browser

[![NPM](https://nodei.co/npm/grunt-contrib-livereload.png?downloads=true)](https://www.npmjs.com/package/grunt-contrib-livereload)

[![apidoc](https://npmdoc.github.io/node-npmdoc-grunt-contrib-livereload/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-grunt-contrib-livereload_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-grunt-contrib-livereload/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-grunt-contrib-livereload/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-grunt-contrib-livereload/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Grunt Team",
        "url": "http://gruntjs.com/"
    },
    "bugs": {
        "url": "https://github.com/gruntjs/grunt-contrib-livereload/issues"
    },
    "contributors": [
        {
            "name": "Frederick Ros",
            "url": "https://github.com/sleeper"
        }
    ],
    "dependencies": {
        "tiny-lr": "~0.0.4"
    },
    "deprecated": "Deprecated in favor of grunt-contrib-watch which now have Livereload support built-in.",
    "description": "Reload assets live in the browser",
    "devDependencies": {
        "grunt": "~0.4.0",
        "grunt-contrib-clean": "~0.4.0",
        "grunt-contrib-internal": "~0.4.2",
        "grunt-contrib-jshint": "~0.1.1",
        "grunt-contrib-nodeunit": "~0.1.2",
        "grunt-simple-mocha": "~0.3.2",
        "mocha": "~1.8.1"
    },
    "directories": {},
    "dist": {
        "shasum": "d7dfaf46bef596e868f354f29a092863080bfeec",
        "tarball": "https://registry.npmjs.org/grunt-contrib-livereload/-/grunt-contrib-livereload-0.1.2.tgz"
    },
    "engines": {
        "node": ">=0.8.0"
    },
    "homepage": "https://github.com/gruntjs/grunt-contrib-livereload",
    "keywords": [
        "gruntplugin",
        "livereload",
        "reload",
        "refresh",
        "websockets"
    ],
    "licenses": [
        {
            "type": "MIT",
            "url": "https://github.com/gruntjs/grunt-contrib-livereload/blob/master/LICENSE-MIT"
        }
    ],
    "main": "Gruntfile.js",
    "maintainers": [
        {
            "name": "sindresorhus",
            "email": "sindresorhus@gmail.com"
        },
        {
            "name": "sleeper",
            "email": "frederick.ros@gmail.com"
        },
        {
            "name": "tkellen",
            "email": "tyler@sleekcode.net"
        },
        {
            "name": "cowboy",
            "email": "cowboy@rj3.net"
        }
    ],
    "name": "grunt-contrib-livereload",
    "optionalDependencies": {},
    "peerDependencies": {
        "grunt": "~0.4.0"
    },
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/gruntjs/grunt-contrib-livereload.git"
    },
    "scripts": {
        "test": "grunt test"
    },
    "version": "0.1.2"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module grunt-contrib-livereload](#apidoc.module.grunt-contrib-livereload)
1.  object <span class="apidocSignatureSpan">grunt-contrib-livereload.</span>utils

#### [module grunt-contrib-livereload.utils](#apidoc.module.grunt-contrib-livereload.utils)
1.  [function <span class="apidocSignatureSpan">grunt-contrib-livereload.utils.</span>livereloadSnippet (req, res, next)](#apidoc.element.grunt-contrib-livereload.utils.livereloadSnippet)
1.  [function <span class="apidocSignatureSpan">grunt-contrib-livereload.utils.</span>startLRServer (grunt, done)](#apidoc.element.grunt-contrib-livereload.utils.startLRServer)



# <a name="apidoc.module.grunt-contrib-livereload"></a>[module grunt-contrib-livereload](#apidoc.module.grunt-contrib-livereload)



# <a name="apidoc.module.grunt-contrib-livereload.utils"></a>[module grunt-contrib-livereload.utils](#apidoc.module.grunt-contrib-livereload.utils)

#### <a name="apidoc.element.grunt-contrib-livereload.utils.livereloadSnippet"></a>[function <span class="apidocSignatureSpan">grunt-contrib-livereload.utils.</span>livereloadSnippet (req, res, next)](#apidoc.element.grunt-contrib-livereload.utils.livereloadSnippet)
- description and source-code
```javascript
function livereloadSnippet(req, res, next) {
  var write = res.write;

  var filepath = url.parse(req.url).pathname;
  filepath = filepath.slice(-1) === '/' ? filepath + 'index.html' : filepath;

  if (path.extname( filepath ) !== '.html') {
    return next();
  }

  res.write = function (string, encoding) {
    var body = string instanceof Buffer ? string.toString() : string;

    body = body.replace(/<\/body>/, function (w) {
      return getSnippet() + w;
    });

    if (string instanceof Buffer) {
      string = new Buffer(body);
    } else {
      string = body;
    }

    if (!this.headerSent) {
      this.setHeader('content-length', Buffer.byteLength(body));
      this._implicitHeader();
    }

    write.call(res, string, encoding);
  };

  next();
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.grunt-contrib-livereload.utils.startLRServer"></a>[function <span class="apidocSignatureSpan">grunt-contrib-livereload.utils.</span>startLRServer (grunt, done)](#apidoc.element.grunt-contrib-livereload.utils.startLRServer)
- description and source-code
```javascript
function startLRServer(grunt, done) {
  var _ = grunt.util._;
  var _server;

  var options = _.defaults(grunt.config('livereload') || {}, {
    port: 35729
  });

  _server = new Server();
  grunt.log.writeln('... Starting Livereload server on ' + options.port + ' ...');
  port = options.port;

  _server.listen(options.port, done);
  return _server;
}
```
- example usage
```shell
...
        files: files
      }
    });
  });

  grunt.registerTask('livereload-start', 'Setup livereload to alert your browser when a file has changed', function () {
    // Start a websocket server in the background
    server = utils.startLRServer(grunt, this.async());
  });
};
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
