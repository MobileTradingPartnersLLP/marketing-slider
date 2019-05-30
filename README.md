# marketing-slider

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

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

# Other notes. 
Currently this uses a local slider module forked from hooper
https://github.com/andyphillips/hooper

I'm creating PRs back to the main branch so hopefully we can just 
``` bash
npm install hooper
```

in the future. If that does not come to pass then you'll need to 
git clone the fork of hooper, npm install/npm run build it and then

``` bash
npm install /path/to/your/build/of/the/clone/hooper --save-dev
```

To make it all work

