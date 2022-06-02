# Scala.js and Vite example

This example project shows how to use [Vite](https://vitejs.dev) together
with [Scala.js](https://scala-js.org).

## Getting started

You need to:

- Install the javascript libraries:

```bash
npm install
```

- Create the bundle:

```bash
./mill --no-server -j 0 -w chart.publicDev
```

- Run Vite dev server (in a separate terminal):

```bash
npm run dev
```

## Production build

You need to run:

```bash
npm run build
```

Now you can find your production build in the `dist` folder.


## Windows Gotcha

It appears that, on windows, the node "spawnSync" commands do no behave in exactly the same way as unix systems. It may be, that in ´vite.config.js´ you need to replace the runMillCommand with;

´´´
function runMillCommand(command) {
  const option = { shell: true }
  const result = spawnSync("mill", ["--no-server", "show", command], option );
  //console.log(result.stdout.toString("utf-8"))
  return JSON.parse(result.stdout.toString("utf-8"));
}
´´´ 
In order, for the mill <-> vite interactions to correctly alias the locations of the js files
