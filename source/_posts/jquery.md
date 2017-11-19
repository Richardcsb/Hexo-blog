---
title: jQuery
date: 2017-11-19 10:43:02
tags: [jQuery]
---
#### Let`s go!
```  
<script>
$(document).ready(function(){
   // 开始写 jQuery 代码...
});
&  
$(function(){
   // 开始写 jQuery 代码...
});
</script>
```  
<!--more-->  
#### jQuery AJAX
##### jQuery load() 方法
把文件 "demo_test.txt" 的内容加载到指定的 <div> 元素中
```  
$("#div1").load("demo_test.txt");
```  
把 "demo_test.txt" 文件中 id="p1" 的元素的内容，加载到指定的 <div> 元素中
```  
$("#div1").load("demo_test.txt #p1");
```  
##### AJAX get() 和 post() 方法
使用 $.get() 方法从服务器上的一个文件中取回数据  
```  
$("button").click(function(){
  $.get("demo_test.php",function(data,status){
    alert("数据: " + data + "\n状态: " + status);
  });
});
```  
用 $.post() 连同请求一起发送数据
```  
$("button").click(function(){
    $.post("/try/ajax/demo_test_post.php",
    {
        name:"菜鸟教程",
        url:"http://www.runoob.com"
    },
        function(data,status){
        alert("数据: \n" + data + "\n状态: " + status);
    });
});
```  
#### 查找过滤

```  
<!-- HTML结构 -->
<ul class="lang">
    <li class="js dy">JavaScript</li>
    <li class="dy">Python</li>
    <li id="swift">Swift</li>
    <li class="dy">Scheme</li>
    <li name="haskell">Haskell</li>
</ul>
```  
根据上面代码用find()查找：  
var ul = $('ul.lang'); // 获得< ul >  
var dy = ul.find('.dy'); // 获得JavaScript, Python, Scheme  
var swf = ul.find('#swift'); // 获得Swift  
var hsk = ul.find('[name=haskell]'); // 获得Haskell  

如果要从当前节点开始向上查找，使用parent()方法：  
var swf = $('#swift'); // 获得Swift  
var parent = swf.parent(); // 获得Swift的上层节点< ul >  
var a = swf.parent('.red'); // 获得Swift的上层节点< ul >，同时传入过滤条件。如果ul不符合条件，返回空jQuery对象   

对于位于同一层级的节点，可以通过next()和prev()方法，例如：  
var swift = $('#swift');  
swift.next(); // Scheme  
swift.next('[name=haskell]'); // 空的jQuery对象，因为Swift的下一个元素Scheme不符合条件[name=haskell]  
swift.prev(); // Python  
swift.prev('.dy'); // Python，因为Python同时符合过滤器条件.dy  

filter()方法可以过滤掉不符合选择器条件的节点：  
var langs = $('ul.lang li'); // 拿到JavaScript, Python, Swift, Scheme和Haskell  
var a = langs.filter('.dy'); // 拿到JavaScript, Python, Scheme  

或者传入一个函数，要特别注意函数内部的this被绑定为DOM对象，不是jQuery对象：  
```  
var langs = $('ul.lang li'); // 拿到JavaScript, Python, Swift, Scheme和Haskell
langs.filter(function () {
    return this.innerHTML.indexOf('S') === 0; // 返回S开头的节点
}); // 拿到Swift, Scheme
```  
map()方法把一个jQuery对象包含的若干DOM节点转化为其他对象：  
```  
var langs = $('ul.lang li');//拿到JavaScript,Python,Swift,Scheme和Haskell
var arr = langs.map(function(){
    return this.innerHTML;
}).get();//用get()拿到包含string的Array:['JavaScript', 'Python', 'Swift', 'Scheme', 'Haskell']
```    
此外，一个jQuery对象如果包含了不止一个DOM节点，first()、last()和slice()方法可以返回一个新的jQuery对象，把不需要的DOM节点去掉：  
var langs = $('ul.lang li'); // 拿到JavaScript, Python, Swift, Scheme和Haskell  
var js = langs.first(); // JavaScript，相当于$('ul.lang li:first-child')  
var haskell = langs.last(); // Haskell, 相当于$('ul.lang li:last-child')  
var sub = langs.slice(2, 4); // Swift, Scheme, 参数和数组的slice()方法一致  

### 操作DOM
#### 设置内容text(),html(),val()
###### 通过 text()、html() 以及 val() 方法来设置内容：
```  
$(document).ready(function(){
  $("#btn1").click(function(){
    $("#test1").text("Hello world!");
  });
  $("#btn2").click(function(){
    $("#test2").html("<b>Hello world!</b>");
  });
  $("#btn3").click(function(){
    $("#test3").val("RUNOOB");
  });
});
```    
###### 带有回调函数的 text() 和 html()：
```  
$("#btn1").click(function(){
    $("#test1").text(function(i,origText){
        return "旧文本: " + origText + " 新文本: Hello world! (index: " + i + ")";
    });
});

$("#btn2").click(function(){
    $("#test2").html(function(i,origText){
        return "旧 html: " + origText + " 新 html: Hello <b>world!</b> (index: " + i + ")";
    });
});
```    
###### 改变（设置）链接中 href 属性的值：
```  
$("button").click(function(){
  $("#runoob").attr("href","http://www.runoob.com/jquery");
});
&
$("button").click(function(){//同时设置href和title属性
    $("#runoob").attr({
        "href" : "http://www.runoob.com/jquery",
        "title" : "jQuery 教程"
    });
});
```    
```  
$("p").append("追加文本");
```  
```  
$("p").prepend("在开头追加文本");
```  
```  
$("#div1").remove();
```  
```  
$("#div1").empty();
```  
```  
$("p").remove(".italic");//删除 class="italic" 的所有 <p> 元素
```  
#### 显示和隐藏DOM
```  
var a = $('a[target=_blank]');
a.hide(); // 隐藏
a.show(); // 显示
```  

#### 修改CSS

###### CSS方法
```  
$("p").css("background-color");//返回指定的 CSS 属性的值
$("p").css("background-color","yellow");//为所有匹配元素设置 background-color 值
$("p").css({"background-color":"yellow","font-size":"200%"});//为所有匹配元素设置 background-color 和 font-size
$('#test-css li.dy>span').css('background-color', '#ffd351').css('color', 'red');

```  

jQuery对象的css()方法可以这么用：
```  
var div = $('#test-div');
div.css('color'); // '#000033', 获取CSS属性
div.css('color', '#336699'); // 设置CSS属性
div.css('color', ''); // 清除CSS属性
```  
为了和JavaScript保持一致，CSS属性可以用'background-color'和'backgroundColor'两种格式。     
###### CSS类
```  
<!-- CSS结构 -->
.important
{
        font-weight:bold;
        font-size:xx-large;
}

.blue
{
        color:blue;
}
```  
```  
$("button").click(function(){
  $("h1,h2,p").addClass("blue");
  $("div").addClass("important");
});
****
$("button").click(function(){
  $("body div:first").addClass("important blue");
});
***
$("button").click(function(){
  $("h1,h2,p").removeClass("blue");
});
****
$("button").click(function(){
  $("h1,h2,p").toggleClass("blue");
});
```  
css()方法将作用于DOM节点的style属性，具有最高优先级。如果要修改class属性，可以用jQuery提供的下列方法：  
```  
var div = $('#test-div');
div.hasClass('highlight'); // false， class是否包含highlight
div.addClass('highlight'); // 添加highlight这个class
div.removeClass('highlight'); // 删除highlight这个class
```  
#### 选择器
> $('p')//元素选择器，选择页面中所有 < p \>元素  
> $('#test')//#id选择器  
> $('.class')//.class选择器  
> $('[name=email]')//按属性查找  
> $('input[name=email]')//组合查找  
> $('tr.red')//组合查找  
> $('p,div')//多项选择器  
> $('ul.land li.lang-javascript');//层级选择，查找ul.land下的li.land-javascript  
> $('form.test p input'); // 多层级选择在form表单选择被< p >包含的< input >  
$('ul.lang li:first-child'); // 子选择器
$('ul.lang li:nth-child(2)'); // 子选择器，选出第N个元素，N从1开始  
$('ul.lang li:nth-child(even)'); // 选出序号为偶数的元素  
$('ul.lang li:nth-child(odd)'); // 选出序号为奇数的元素  
$('div:visible'); // 所有可见的div  
> $("*")//选取所有元素  
> $("this")//选取当前html元素  
> $("p.intro")//选取class为intro的< p >元素
> $("p:first")//选取第一个 < p > 元素  
> $("ul li:first")//选取第一个 < ul > 元素的第一个 < li > 元素    
> $("[href]")//选取带有 href 属性的元素  
> $("a[target='_blank']")//选取所有 target 属性值等于 "_blank" 的< a >元素  
> $(":button")//选取所有 type="button" 的 < input > 元素 和 < button > 元素  
> $("tr:even")//选取偶数位置的 <tr> 元素  
> $("tr:odd")//选取奇数位置的 <tr> 元素  

#### jQuery 事件
click()  
```  
$("p").click(function(){
  $(this).hide();
});
```    
dblclick()
```  
$("p").dblclick(function(){
  $(this).hide();
});
```  
mouseenter()  
```  
$("#p1").mouseenter(function(){
    alert('您的鼠标移到了 id="p1" 的元素上!');
});
```    
mouseleave()
```  
$("#p1").mouseleave(function(){
    alert("再见，您的鼠标离开了该段落。");
});
```  
mousedown()  
```  
$("#p1").mousedown(function(){
    alert("鼠标在该段落上按下！");
});
```  
mouseup()
```  
$("#p1").mouseup(function(){
    alert("鼠标在段落上松开。");
});
```  
hover()
```  
$("#p1").hover(
    function(){
        alert("你进入了 p1!");
    },
    function(){
        alert("拜拜! 现在你离开了 p1!");
    }
);
```  
focus()
```  
$("input").focus(function(){
  $(this).css("background-color","#cccccc");
});
```  
blur()
```  
$("input").blur(function(){
  $(this).css("background-color","#ffffff");
});
```  
#### jQuery 效果
[淡入淡出](http://www.runoob.com/jquery/jquery-fade.html)
