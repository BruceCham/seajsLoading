seajsLoading
============

seajs加载执行顺序

````html
html文件
    seajs.config({
        alias: {
        	"a":"/seajs/js/a.js",
    			"b":"/seajs/js/b.js",
    			"c":"/seajs/js/c.js"
        },
		    preload: ["b","c"]
    });
    seajs.use("",function(){
		console.log("doing use")
	});
------------console-----------
b fuck to loading 
c fuck to loading 
doing use
------------end-----------

或
    seajs.config({
        alias: {
        	"a":"/seajs/js/a.js",
    			"b":"/seajs/js/b.js",
    			"c":"/seajs/js/c.js"
        }
    });
    seajs.use("a",function(a){
		console.log("doing use")
	});
------------console-----------
a fuck to loading 
b fuck to loading 
b fuck to say hello 
c fuck to loading 
c fuck to say hello
doing use
------------end-----------

````
a.js文件

````javascript
define(function(require,exports,module){
	console.log("a fuck to loading")
	var b = require('b');	
	b.hello();
	var c = require('c');
	c.hello();
})
````
b.js文件
````javascript
define(function(require,exports,module){
	console.log('b fuck to loading');
	exports.hello = function(){
		console.log("b fuck to say hello")
	}
})
````
c.js文件 
````javascript
define(function(require,exports,module){
	console.log('c fuck to loading');
	exports.hello = function(){
		console.log("c fuck to say hello")
	}
})

````
