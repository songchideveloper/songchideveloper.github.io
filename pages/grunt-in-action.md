
### Install Grunt
#### Install the CLI
`npm install -g grunt-cli`


### Install Yeoman
#### 1. Install Yeoman
`npm install -g yo`
#### 2. Install Yeoman Generator
Example to install the 'webapp' generator   
`npm install -g generator-webapp`
#### 3. Generate the project
`yo webapp <my-app-name>`


### `Gruntfile.js` Config
#### Config the source and distribution file paths
```javascript
var config = {
  app: 'app',
  dist: 'dist'
}
```

### Config the `initConfig()`
Put all the init config in to the `initConfig()` as an obj:
```javascript
grunt.initConfig({
  ....
})
```

### Assign the config path
```javascript
grunt.initConfig({
  config: config,
  
  ...
})
```


### define the __copy__, copy files from the `src` to the `dest`
```javascript
grunt.initConfig({
  ...
  
  copy: {
    dist_html: {
      src: '<%= config.app %>/index.html',
      dest: '<%= config.dist %>/index.html'
    },
    dist_js: {
      src: '<%= config.app %>/js/index.js',
      dest: '<%= config.dist %>/js/index.js'
    }
  },
  
  ...
})
```
