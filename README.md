[![Build Status](https://travis-ci.org/webrtc/adapter.svg)](https://travis-ci.org/webrtc/adapter)

# WebRTC adapter #
adapter.js is a shim to insulate apps from spec changes and prefix differences. In fact, the standards and protocols used for WebRTC implementations are highly stable, and there are only a few prefixed names. For full interop information, see [webrtc.org/web-apis/interop](https://www.webrtc.org/web-apis/interop).

## Install ##

#### NPM
```bash
npm install webrtc-adapter
```

#### Bower
```bash
bower install webrtc-adapter
```

## Usage ##
##### NPM
Copy to desired location in your src tree or use a minify/vulcanize tool (node_modules is usually not published with the code).
See [webrtc/samples repo](https://github.com/webrtc/samples/blob/gh-pages/package.json) as an example on how you can do this.

#### Prebuilt releases
##### Web
In the [gh-pages branch](https://github.com/webrtc/adapter/tree/gh-pages) prebuilt ready to use files can be downloaded/linked directly.
Latest version can be found at https://webrtc.github.io/adapter/adapter-latest.js.
Specific versions can be found at https://webrtc.github.io/adapter/adapter-N.N.N.js, e.g. https://webrtc.github.io/adapter/adapter-1.0.2.js.

##### Bower
You will find `adapter.js` in `bower_components/webrtc-adapter/`.

##### NPM
In node_modules/webrtc-adapter/out/ folder you will find 4 files:
* `adapter.js` - includes all the shims and is visible in the browser under the global `adapter` object (window.adapter).
* `adapter_no_edge.js` - same as above but does not include the Microsoft Edge (ORTC) shim.
* `adapter_no_edge_no_global.js` - same as above but is not exposed/visible in the browser (you cannot call/interact with the shims in the browser).
* `adapter_no_global.js` - same as `adapter.js` but is not exposed/visible in the browser (you cannot call/interact with the shims in the browser).

Include the file that suits your need in your project.

## Development ##
Detailed information on developing in the [webrtc](https://github.com/webrtc) github repo can be found in the [WebRTC GitHub repo developer's guide](https://docs.google.com/document/d/1tn1t6LW2ffzGuYTK3366w1fhTkkzsSvHsBnOHoDfRzY/edit?pli=1#heading=h.e3366rrgmkdk).

Head over to [test/README.md](https://github.com/webrtc/samples/blob/gh-pages/test/README.md) and get started developing.

## Publish a new version ##
* Go the the adapter repository root directory
* Make sure your repository is clean, i.e. no untracked files etc. Also check that you are on the master branch and have pulled the latest changes.
* Depending on the impact of the release, either use `patch`, `minor` or `major` in place of `<version>`. Run `npm version <version> -m 'bump to %s'` and type in your password lots of times (setting up credential caching is probably a good idea).
* Create and merge the PR if green in the GitHub web ui
* Go to the releases tab in the GitHub web ui and edit the tag.
* Add a summary of the recent commits in the tag summary and a link to the diff between the previous and current version in the description, [example](https://github.com/webrtc/adapter/releases/tag/v3.4.1).
* Go back to your checkout and run `git pull`
* Run `npm publish` (you need access to the [webrtc-adapter npmjs package](https://www.npmjs.com/package/webrtc-adapter))
* Done! There should now be a new release published to NPM and the gh-pages branch.

Note: Currently only tested on Linux, not sure about Mac but will definitely not work on Windows.

### Publish a hotfix patch versions
In some cases it may be necessary to do a patch version while there are significant changes changes on the master branch.
To make a patch release,
* checkout the latest git tag using `git checkout tags/vMajor.minor.patch`.
* checkout a new branch, using a name such as patchrelease-major-minor-patch. 
* cherry-pick the fixes using `git cherry-pick some-commit-hash`.
* run `npm version patch`. This will create a new patch version and publish it on github.
* check out the branch created earlier and publish the new version using `npm publish`.
* the branch can now safely be deleted. It is not necessary to merge it into the main branch since it only contains cherry-picked commits.
