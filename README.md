# note
个人工作以及项目遇到的知识点

[概述](#1)

1.对于多个ajax请求

  （1）当需要在所有请求之后，拿到所有数据，不保证请求返回顺序
  ```javascript
  var counts = 0;
  var callBack = function() { 
      counts++;
      //判断是否完全返回完毕
      if (counts === ajax.length){
      }
  }
  var doAjax = function(){
      ajax({
        success: function() {
            callBack();
        }
      });
  }; //执行ajax请求
  ```
  
  （2）当需要在所有请求之后，拿到所有数据，保证请求返回顺序
  ```javascript
  function nextRegister(){
        var args = arguments;
        var counts = 0;
        var action = function(cb) {
            setTimeout(function() { console.log(counts); cb(); },500);
        };
        var next = function(){
            counts++;
            if(counts < args.length) {
                action(next);
            }
        }
        if(counts < args.length) {
            action(next);
        }
    }
    nextRegister(url1,url2,url3);
  ```
  
  2.函数节流与防抖的简单实现
    （1）节流
    ```javascript
    var throttle = function(func, delay){
        var prev = Date.now();
        return function() {
            var context = this;
            var args = arguments;
            var now = Date.now();
            if(now - prev >= delay){
                func.apply(context, args);
                prev = Date.now();
            }
        }
    };
    var imgThrottle = throttle(节流的函数名称, 500);
    ```
  （2）防抖
  
  <a name="1">第一段</a>
  
  ```javascript
  function debounce(method, context, args) {
      clearTimeout(method.tId);
      method.tId = setTimeout(function() {
          console.log('load');
          method.call(context,args);
      }, 1000);
  }
  debounce(防抖的函数名称, 上下文环境, 参数);
  ```
