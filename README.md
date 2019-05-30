# marketing-slider

> A multiwidget slider wrapper

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).

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