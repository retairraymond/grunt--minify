1. tool and packages
  - Grunt
  - grunt-contrib-htmlmin
  - grunt-contrib-uglify
  - Grunt and Gunt's packages 通过npm安装、管理；
2. 配置package.json文件
   ```
   {
	  "name": "icemapp",
	  "version": "0.0.0",
	  "dependencies": {},
	  "devDependencies": {
	    "gifsicle": "0.1.3",
	    "grunt": "^0.4.5",
	    "grunt-autoprefixer": "^0.7.3",
	    "grunt-concurrent": "^0.5.0",
	    "grunt-contrib-clean": "^0.5.0",
	    "grunt-contrib-compass": "^0.7.2",
	    "grunt-contrib-concat": "^1.0.0",
	    "grunt-contrib-connect": "^0.7.1",
	    "grunt-contrib-copy": "^0.5.0",
	    "grunt-contrib-cssmin": "^0.9.0",
	    "grunt-contrib-htmlmin": "^0.3.0",
	     // 等等其他需要的packages
	  }
	}
   ```
3. 配置Gruntfile.js文件
  - *Gruntfile。js文件中代码结构*
	```
	module.exports = function(grunt) {
	  // 1.配置任务
	  grunt.initConfig({
	    pkg: grunt.file.readJSON('package.json'),
	    htmlmin: {
	    	options: {
	    		// 用来指定覆盖内置属性的默认值
	    	},
	    	target: {
	    	 	// ...
	    	}
	    },
	    uglify: {
	      target: {
	        // ...
	      }
	    }
	  });
      // 2.加载所需插件	
	  grunt.loadNpmTasks('grunt-contrib-htmlmin');
	  grunt.loadNpmTasks('grunt-contrib-uglify');
		
	  // 3.注册任务
	  grunt.registerTask('htmlmin',['htmlmin']);
	  grunt.registerTask('jsmini', ['uglify']);

	};
	```
  - *配置任务部分的示例代码*
	```
	//压缩所有的html文件
    htmlmin: {
      options: {
        removeComments: true,
        collapseWhitespace: true
      },
      target: {
        expand: true,
        cwd: 'app/',
        src: '**/*.html',
        dest: 'appmin/'
      }
    },

    //压缩所有的js文件
    uglify: {
      target: {
        expand: true,
        cwd: 'app',
        src: '**/*.js',
        dest: 'appmin/'
      }
    }
	```
	  + **注意**
	    * 每个task中至少需要一个target；
  - *Grunt的文件系统*
	  + grunt绝大多数工作内容是处理文件，其中文件部分，可以使用三种格式表示---简洁格式、文件对象格式、文件数组格式；
	  + 如果要处理大量打个文件时，可以将expand属性值设置为true；来开启额外的属性；
	    * cwd --- 设置相对路径；
	    * src --- 相对于cwd路径的匹配模式；
        * dest --- 目标文件路径；
	    * ext --- 设置文件的扩展名；

4. cmd
  - grunt taskName
    + grunt htmlmin
    + grunt uglify
