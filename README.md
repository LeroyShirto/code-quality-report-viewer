# Code Climate Code Quality Report Viewer

To analyse code run the command below in the root of your application repository

```sh
codeclimate analyze -f json | jq -c 'map(select(.type | test("issue"; "i")))' > code-quality-report.json
```

Copy the contents of `code-quality-report.json` into the text field of the vue app

Code Quality documentation: https://docs.codeclimate.com/docs

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
