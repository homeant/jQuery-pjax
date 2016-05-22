#jQuery-pjax

            .--.
           /    \
          ## a  a
          (   '._)
           |'-- |
         _.\___/_   ___pjax___
       ."\> \Y/|<'.  '._.-'
      /  \ \_\/ /  '-' /
      | --'\_/|/ |   _/
      |___.-' |  |`'`
        |     |  |
        |    / './
       /__./` | |
          \   | |
           \  | |
           ;  | |
           /  | |
     jgs  |___\_.\_
          `-"--'---'
          
[pjax初始版本](https://github.com/defunkt/jquery-pjax)


##此处版本主要做了如下改动：


1. 加入loadAjaxScript方法，改方法可以动态获取js,并执行
```
var scripts = ["js/container.1.js"];

$.pjax.loadAjaxScript(scripts,function(){

	$(function(){
	
		$.app.msg("我适合做插件");
		
		alert("我最后加载");
		
	});
	
});
```

2. 在原先基础上加入监听，保证用户强刷浏览器页面直接跳转至pjax页面，该版本不影响原先pjax的使用

```
$(document).pjax("a", "#pjax-container", {

	//maxCacheLength: 0, //正式环境，请修改
	
	//fragment: "#container",//从哪个元素中获取内容
	
	//自定义规则,和enableHash属性需同时出现，点击元素中需出现hash属性
	
	//此规则针对于hash属性，返回真实的url
	
	//注：下面规则暂不支持带参数的url，可自定义扩展
	
	contentUrl: function(url) {
	
		if (!url.match(/^page\//)) return false;
		
		var path = document.location.pathname;
		
		if (path.match(/index\.html/)){
		
			return path.replace(/index\.html/, url.replace(/^page\//, '') + '.html');
			
		}
		
		return path + "?" + url.replace(/\//, "=");
		
	},
	
	enableHash:true,
	
	//defaultUrl: 'page/container3'//加载首页默认加载的页面
	
});
```

3. 去除原先pjax中的form提交。