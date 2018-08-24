# css命名实践
## 命名规则
采用表示层级嵌套关系的长命名。当子孙模块超过4级或以上的时候，考虑在祖先模块内具有识辨性的独立缩写作为新的子孙模块
``` html
    <div class="modulename">
    <div class="modulename_cover"></div>
    <div class="modulename_info">
        <div class="modulename_info_user">
            <div class="modulename_info_user_img">
                <img src="" alt="">
                <!-- 这个时候 miui 为 modulename_info_user_img 首字母缩写-->
                <div class="miui_tit"></div>
                <div class="miui_txt"></div>
                ...
            </div>
        </div>
        <div class="modulename_info_list"></div>
    </div>
</div>
```


## 分隔符

### 中划线   表示层级关系    [ list-item ] 
``` html
    <div class="box">
    	<ul class="box-list">
       	 	<li class="box-list-item"></li>
       	 	<li class="box-list-item"></li>
         	        <li class="box-list-item"></li>
   	        </ul>
    </div>
```

### 下划线    表示不同的状态    [list_item]
``` html
<div class="box">
    	<button class="box-btn box-btn_default" type="button"></button>
    	<button class="box-btn" type="button"></button>
	</div>
```

### 驼峰命名    表示因样式的需要不得不增加的HTML结构 [boxWrap]

``` html
<div class="boxWrap">
    <div class="box">
        <div class="boxInner"></div>
    </div>
</div>
```
1. 在外层增加结构，可以增加Wrap
2. 在内层增加结构，可以增加Inner


## 模块命名

* 全站公告模块：以 mod_ 开头
``` html
<div class="mod_yours"></div>
```
* 业务公告模块：以 业务名 _mod_ 开头
``` html
<div class="paipai_mod_yours"></div>
```



## 实例
``` html
    <header class="hd">
    <nav class="hd-navbar m-navbar m-varbar_primary">
        <div class="hd-navbar-tel">联系方式：400-888-8888</div>
        <ul class="hd-navbar-nav">
            <li class="Hnn-itm m-btn m-btn_info"><a href="#">登录</a></li>
            <li class="Hnn-itm m-btn"><a href="#">快速注册</a></li>
            <li class="Hnn-itm m-btn"><a href="#">关于</a></li>
            <li class="Hnn-itm m-btn"><a href="#">帮助</a></li>
        </ul>
    </nav>
    ...
</header>
```