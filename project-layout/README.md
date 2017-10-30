# Cisco Spark Web Project Layouts

*How we Mono Repo*

## Table of Contents

1. Inspiration
1. Layout
1. Tooling

## Inspiration

Most of our projects have embraced the mono repo project layout. I won't go into too much detail here since there are plenty of other articles written about this topic, but we primarily us it because it provides us with a logical way to encapsulate features without the need to coordinate changes across repos.

Usually for JS and node/npm based projects the go to tools involve [`lerna`](https://github.com/lerna/lerna), and that is where we started. After working with it for months we realized that it was a bit too heavy weight for our projects, and opted to change to the [`alle`](https://github.com/boennemann/alle) layout. It's much more lightweight and uses `npm` and `node` built in module resolution.

## Layout

With the `alle` setup, our projects generally look something like this:

``` text
- package.json
- node_modules/
- scripts/
  - webpack/
  - build/
  - ...
- packages/
  - node_modules/
    - some-react-package/
    - some-redux-module/
    - some-container/
      - package.json
      - src/ *where the package code actually lives*
```

All of our actual packages are stored under `packages/node_modules` and all of our dependencies are declared globally in the top `package.json` file and installed in the room `node_modules` directory. At runtime or build time, we use our tooling stack to resolve the dependencies of each package to the modules installed in the root.

## Tooling

We don't have a separate tooling project just yet, but you can see `alle` in action here:

- Cisco Spark React Widgets <https://github.com/ciscospark/react-ciscospark>
- Cisco Spark JS SDK <https://github.com/ciscospark/spark-js-sdk>
