
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

#### Config the `initConfig()`
Put all the init config in to the `initConfig()` as an obj:
```javascript
grunt.initConfig({
  ....
})
```

#### Assign the config path
```javascript
grunt.initConfig({
  config: config,
  
  ...
})
```


#### Define the __copy__, copy files from the `src` to the `dest`
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

Here is a way to add another `files` array property to refactor the `copy` property for the convenience of multiple sets of src/dest:   
```javascript
grunt.initConfig({
  ...
  
  copy: {
    dist: {
      files: [
        {
            src: '<%= config.app %>/index.html',
            dest: '<%= config.dist %>/index.html'
        },
        {
            src: '<%= config.app %>/js/index.js',
            dest: '<%= config.dist %>/js/index.js'
        }
      ]
        
    }
  },
  
  ...
})
```

We can move further, to change the `files` arrays property to obj key-value property, so that we don't have to specify the _src_ and _dest_. By default, the __key__ is the `dest` and the __value__ is the `src`.
```javascript
grunt.initConfig({
  ...
  
  copy: {
    dist: {
      files: {
        '<%= config.app %>/index.html': '<%= config.dist %>/index.html',
        '<%= config.app %>/js/index.js': dest: '<%= config.dist %>/js/index.js'
      }
    }
  },
  
  ...
})
```

#### Define the __clean__ property, to clean up the specific files

```javascript
grunt.initConfig({
  ...
  
  clean: {
    dist: {
      src: ['<%= config.dist %>/index.html', '<%= config.dist %>/js/index.js']
    }
  },
  
  ...
})
```
It is tedious when you have to specify the exactly path to clean up the files, we can refactor this.
`**` for all the folder and `*` for all the files.
grunt.initConfig({
  ...
  
  clean: {
    dist: {
      src: ['<%= config.dist %>/**/*']
    }
  },
  
  ...
})
```
