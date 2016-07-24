
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
``` javascript
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
If we want to only delete the files not the folder, then we can use `filter: 'isFile'`    
``` javascript
grunt.initConfig({
  ...
  
  clean: {
    dist: {
      src: ['<%= config.dist %>/**/*'],
      filter: 'isFile'
    }
  },
  
  ...
})
```
Or we can write our own filter like below:   
``` javascript
grunt.initConfig({
  ...
  
  clean: {
    dist: {
      src: ['<%= config.dist %>/**/*'],
      filter: function (filepath) {
          return (!grunt.file.isDir(filepath));
      }
    }
  },
  
  ...
})
```

### Here is the way to use the `expand` property in the `files` object (we need the array format to represent the `files`).
- `expand: true` to enable the expand.
- `cwd` to specify the `src` prefix path
- `ext` to modify the file extention when copied to the destination
- `extDot:first` or `extDot:last` to specify which dot is the start point to modify the file extension.
- `flatten:true` to flatten the sub-folders, just put the file to the path specified in the `dest`
- `rename:function(dest, src){}` to rename the filename in copied to the destination.
```javascript
grunt.initConfig({
  ...
  
  copy: {
    dist: {
      files: [
        {
          expend: true,
          cwd: '<%=config.app%>/',
        }
      ]
    }
  },
  
  ...
})
```
