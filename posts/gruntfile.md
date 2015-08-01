---
title: Hngh!, Or, What's a Grunt File, Anyway?
tags: grunt, javascript, hack reactor, automation, node
published: true
---

edit

Sometimes, you find yourself doing the same things over and over (and when you code), like linting, minifying / uglifying, or installing from several different package managers (npm, bower, etc). It can be annoying and time-consuming to do all that manually several times. Wouldn't it be awesome if there was a tool that allowed us to automate just about anything?

##Enter [Grunt.](http://gruntjs.com/)

Here's an example Gruntfile from one of my team projects at Hack Reactor:

```
module.exports = function (grunt) {

  // Project configuration.
  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),
    githooks: {
      all: {
        'pre-commit': 'checkSyntax'
      }
    },
    jshint: {
      files: [
        'Gruntfile.js', 'server.js', 'server/**.js', 'client/**.js', '!client/lib/**.js'
      ],
      options: {
        globals: {
          jQuery: true
        }
      }
    },
    ngAnnotate: {
      options: {
        add: true,
        expand: false,
        singleQuotes: true
      },
      skillit: {
        files: {
          'client/build/<%= pkg.name %>.min.js': [
            'client/app/factories/factories.js',
            'client/app/controllers/loginCtrl.js',
            'client/app/controllers/signupCtrl.js',
            'client/app/controllers/exploreCtrl.js',
            'client/app/controllers/profileCtrl.js',
            'client/app/app.js',
            'client/app/**.js',
            '!client/lib/**'
          ],
        },
      }
    },
    uglify: {
      options: {
        banner: '/*! <%= pkg.name %> <%= grunt.template.today("yyyy-mm-dd") %> */\n',
        options: {
          compress: true,
          mangle: true,
          sourceMap: true
        }
      },
      build: {
        src: [
          'client/build/<%= pkg.name %>.min.js'
        ],
        dest: 'client/build/<%= pkg.name %>.min.js'
      }
    },
    nodemon: {
      dev: {
        script: 'server.js'
      }
    },
    watch: {
      files: ['<%= jshint.files %>'],
      tasks: ['jshint']
    },
    concurrent: {
      dev: {
        tasks: ['jshint', 'nodemon', 'watch'],
        options: {
          logConcurrentOutput: true
        }
      }
    }
  });

  // Load the plugin that provides the "uglify" task.
  grunt.loadNpmTasks('grunt-contrib-uglify');
  grunt.loadNpmTasks('grunt-ng-annotate');
  grunt.loadNpmTasks('grunt-githooks');
  grunt.loadNpmTasks('grunt-contrib-watch');
  grunt.loadNpmTasks('grunt-nodemon');
  grunt.loadNpmTasks('grunt-contrib-jshint');
  grunt.loadNpmTasks('grunt-concurrent');

  //tasks
  grunt.registerTask('checkSyntax', ['jshint']);
  grunt.registerTask('build', ['checkSyntax', 'ngAnnotate', 'uglify']);

  grunt.registerTask('magic', '', function () {
    var taskList = [
      'concurrent',
      'jshint',
      'nodemon',
      'watch'
    ];
    grunt.task.run(taskList);
  });

  grunt.registerTask('default', ['githooks', 'magic']);
};

```

When you run "grunt" in the command line, this'll do a number of things: a) make it so that each time your files must pass an automatic lint before they can be git committed; b) automagically watch all files in the project, linting and restarting the server on each change

It also gives the command "grunt build," which lints, applies some specific Angular code fixes, and uglifies client-side code so that it's easier to serve in production.

Let's step through it:

###1. Wrapper
The first thing every gruntfile needs is a wrapper function.
```
module.exports = function (grunt) {
///all grunt stuff here
}
```

###2. Config
The first thing inside the wrapper function is your config initialization. This will allow us to declare our package information (in this case, using NPM's "package.json"), as well as declare what each of our tasks will actually *do*.
```
grunt.initConfig({
//any setup, as well as what your various tasks will do, goes here
})
```
###3.Dependencies
The series of grunt modules your gruntfile requires to run. Each of these must be installed using npm in order to be used.
```
 grunt.loadNpmTasks('gruntModuleNameHere');
```

###4.Tasks
Here's where you set your bound task names. The "default" task list will run when you type "grunt" in the command line.
```
grunt.registerTask('default', [
//tasks you wish to bind to the given task name go here
]);
```
