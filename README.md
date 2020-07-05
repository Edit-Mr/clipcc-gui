<div align="center">
<img src="https://clipsrc.blestudio.com/clip-logo-with-text.png"/>

# clipcc-gui
![](https://img.shields.io/travis/clipteam/clipcc-gui.svg?style=flat-square)

</div>

#### ClipCC is a powerful scratch-project editor based on clipcc-gui which was created by MIT. And it migrates a lot of function from ClipCC 1.x. 

## Links
### [clipcc-l10n](https://github.com/Clipteam/clipcc-l10n)

### [clipcc-block](https://github.com/Clipteam/clipcc-block)

### [clipcc-vm](https://github.com/Clipteam/clipcc-vm)

## Installation
This requires you to have Git and Node.js installed.

In your own node environment/application:
```bash
yarn install https://github.com/Clipteam/clipcc-gui.git
```
If you want to edit/play yourself:
```bash
git clone https://github.com/Clipteam/clipcc-gui.git
cd clipcc-gui
yarn install
```

## Getting started
Running the project requires Node.js to be installed.

## Running
Open a Command Prompt or Terminal in the repository and run:
```bash
yarn start
```
Then go to [http://localhost:8601/](http://localhost:8601/) - the playground outputs the default GUI component

## Developing alongside other Scratch repositories

### Getting another repo to point to this code


If you wish to develop `clipcc-gui` alongside other scratch repositories that depend on it, you may wish
to have the other repositories use your local `clipcc-gui` build instead of fetching the current production
version of the clipcc-gui that is found by default using `yarn install`.

Here's how to link your local `clipcc-gui` code to another project's `node_modules/clipcc-gui`.

#### Configuration

1. In your local `clipcc-gui` repository's top level:
    1. Make sure you have run `yarn install`
    2. Build the `dist` directory by running `BUILD_MODE=dist yarn run build`
    3. Establish a link to this repository by running `yarn link`

2. From the top level of each repository (such as `scratch-www`) that depends on `clipcc-gui`:
    1. Make sure you have run `yarn install`
    2. Run `yarn link clipcc-gui`
    3. Build or run the repositoriy

#### Using `yarn run watch`

Instead of `BUILD_MODE=dist yarn run build`, you can use `BUILD_MODE=dist yarn run watch` instead. This will watch for changes to your `clipcc-gui` code, and automatically rebuild when there are changes. Sometimes this has been unreliable; if you are having problems, try going back to `BUILD_MODE=dist yarn run build` until you resolve them.

#### Oh no! It didn't work!

If you can't get linking to work right, try:
* Follow the recipe above step by step and don't change the order. It is especially important to run `yarn install` _before_ `yarn link`, because installing after the linking will reset the linking.
* Make sure the repositories are siblings on your machine's file tree, like `.../.../MY_SCRATCH_DEV_DIRECTORY/clipcc-gui/` and `.../.../MY_SCRATCH_DEV_DIRECTORY/scratch-www/`.
* Consistent node.js version: If you have multiple Terminal tabs or windows open for the different Scratch repositories, make sure to use the same node version in all of them.
* If nothing else works, unlink the repositories by running `yarn unlink` in both, and start over.

## Testing
### Documentation

You may want to review the documentation for [Jest](https://facebook.github.io/jest/docs/en/api.html) and [Enzyme](http://airbnb.io/enzyme/docs/api/) as you write your tests.

See [jest cli docs](https://facebook.github.io/jest/docs/en/cli.html#content) for more options.

### Running tests

*NOTE: If you're a windows user, please run these scripts in Windows `cmd.exe`  instead of Git Bash/MINGW64.*

Before running any test, make sure you have run `yarn install` from this (clipcc-gui) repository's top level.

#### Main testing command

To run linter, unit tests, build, and integration tests, all at once:
```bash
yarn test
```

#### Running unit tests

To run unit tests in isolation:
```bash
yarn run test:unit
```

To run unit tests in watch mode (watches for code changes and continuously runs tests):
```bash
yarn run test:unit -- --watch
```

You can run a single file of integration tests (in this example, the `button` tests):

```bash
$(yarn bin)/jest --runInBand test/unit/components/button.test.jsx
```

#### Running integration tests

Integration tests use a headless browser to manipulate the actual html and javascript that the repo
produces. You will not see this activity (though you can hear it when sounds are played!).

Note that integration tests require you to first create a build that can be loaded in a browser:

```bash
yarn run build
```

Then, you can run all integration tests:

```bash
yarn run test:integration
```

Or, you can run a single file of integration tests (in this example, the `backpack` tests):

```bash
$(yarn bin)/jest --runInBand test/integration/backpack.test.js
```

If you want to watch the browser as it runs the test, rather than running headless, use:

```bash
USE_HEADLESS=no $(yarn bin)/jest --runInBand test/integration/backpack.test.js
```

## Troubleshooting

### Ignoring optional dependencies

When running `yarn install`, you can get warnings about optionsl dependencies:

```
npm WARN optional Skipping failed optional dependency /chokidar/fsevents:
npm WARN notsup Not compatible with your operating system or architecture: fsevents@1.2.7
```

You can suppress them by adding the `no-optional` switch:

```
yarn install --no-optional
```

Further reading: [Stack Overflow](https://stackoverflow.com/questions/36725181/not-compatible-with-your-operating-system-or-architecture-fsevents1-0-11)

### Resolving dependencies

When installing for the first time, you can get warnings which need to be resolved:

```
npm WARN eslint-config-scratch@5.0.0 requires a peer of babel-eslint@^8.0.1 but none was installed.
npm WARN eslint-config-scratch@5.0.0 requires a peer of eslint@^4.0 but none was installed.
npm WARN scratch-paint@0.2.0-prerelease.20190318170811 requires a peer of react-intl-redux@^0.7 but none was installed.
npm WARN scratch-paint@0.2.0-prerelease.20190318170811 requires a peer of react-responsive@^4 but none was installed.
```

You can check which versions are available:

```
yarn view react-intl-redux@0.* version
```

You will neet do install the required version:

```
yarn install  --no-optional --save-dev react-intl-redux@^0.7
```

The dependency itself might have more missing dependencies, which will show up like this:

```
user@machine:~/sources/scratch/clipcc-gui (491-translatable-library-objects)$ yarn install  --no-optional --save-dev react-intl-redux@^0.7
clipcc-gui@0.1.0 /media/cuideigin/Linux/sources/scratch/clipcc-gui
├── react-intl-redux@0.7.0
└── UNMET PEER DEPENDENCY react-responsive@5.0.0
```

You will need to install those as well:

```
yarn install  --no-optional --save-dev react-responsive@^5.0.0
```

Further reading: [Stack Overflow](https://stackoverflow.com/questions/46602286/npm-requires-a-peer-of-but-all-peers-are-in-package-json-and-node-modules)


## Publishing to GitHub Pages
You can publish the GUI to github.io so that others on the Internet can view it.
[Read the wiki for a step-by-step guide.](https://github.com/LLK/clipcc-gui/wiki/Publishing-to-GitHub-Pages)

## Want to add more function?

If you want us to add more function in clipcc3, you can add a issue to tell us what kind of function do you like.

## Contact us

You can contact us by sending an email to [clipteam@codingclip.com](mailto:clipteam.codingclip.com). We are looking forward to you feedback.
## Donate

Not now

<div align="center">

#### Copyright © *Clipteam* All rights reserved.

</div>
