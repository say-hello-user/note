# note
个人工作以及项目遇到的知识点

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
  
