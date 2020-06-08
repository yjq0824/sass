# 关于sass

## sass的主要作用



```通俗的说，‘
	CSS预处理器用一种专门的编程语言，进行Web页面样式设计，然后再编译成正常的CSS文件，以供项目使用。CSS预处理器为CSS增加一-些编程的特性,无需考虑浏览器的兼容性问题”，例如你可以在CSS中使用变量、简单的逻辑程序、函数等等在编程语言中的一-些基本特性，可以让你的CSS更加简洁、适应性更强、可读性更佳，更易于代码的维护等诸多好处。
```

## sass与scss

```Sass和SCSS其实是同- -种东西，我们平时都称之为Sass,
两者之间不同之处有以下两点:

文件扩展名不同，Sass 是以“.sass”后缀为扩展名，而SCSS是以“.scss”后缀为扩展名

语法书写方式不同，Sass 是以严格的缩进式语法规则来书写，不带大括号({)和分号(;)，而SCSS的语法书写和我们
的CSS语法书写方式非常类似。
```

## sass的安装	

#### 依赖于ruby环境

```
1.检测ruby

ruby -v  .....检测当前你的电脑的ruby版本

2.下载ruby
https://rubyinstaller.org/downloads/

3.安装
安装时，记得勾选写入环境变量；其他默认即可

4.安装sass
windows终端：
gem install sass
Mac终端：
sudo gem install sass

5.查看sass版本号
sass -v

6.更新和卸载sass
更新:gem update sass
卸载：gem uninstall sass

7.进入sass终端
sass -i （可运行sass语法，用于测试sass语法）

```

#### sass的编译

```
1.文件的编译：
sass (要编译的scss文件).../test.scss:(编译完的css文件存储地址).../test.css

例子：sass .../test.scss:.../test.css

2.实时监控文件：
sass --watch(要编译的scss文件).../test.scss：(编译完的css文件存储地址).../test.css

例子：sass --watch.../test.scss:.../test.css

3.实时监控文件夹：（cd  你要进入的文件夹）
sass --watch 存储.scss的文件夹：存储.css的文件夹

例子：sass --watch sass：css

```

### sass编译为css后的输出格式

```
1.compressed（压缩输出方式）
2.expanded（展开输出方式）
3.compact（紧凑输出方式）
4.nested（嵌套输出方式）

语法：sass --watch scss文件：css文件 --style XXXX（上述方式）![]()
```

### .scss文件的注释方式

```
单行注释：
/* */
多行注释：(编译之后不保留)
//
（注意！：压缩输出方式会去掉注释）

强制注释：
/*!   */

```







## sass主要语法

### 1.变量与嵌套



##### 定义变量

```
$color:#ffff

.div1{
    background:$color
}
```

##### 选择器嵌套

```
.div1{	
		.aa{

		..........

		}

}
```

##### 引用父类选择器

```
.div1{
    &：hover{
        
    }
}
等于：
.div1:hover{
    
}
```

##### 属性嵌套

```
.div1{
    backgrounf:{
        color:...
        iamge:...
        position:...
    };
    
    border:{
        left:{
            color:transparent;
            style:...;    
        }
    }
}
```

##### 变量作为属性

```
$bg:background

.div1{
    #{$bg}:#ffff;
}
```



---





### 2.mix in 混合

```
不带参数：
@mixin aa{
    width:100px;
	height；100px；
}


直接套用：
.div1{
	@include aa；
    
}

带参数：
@mixin aa（$num,$color）{
    width:$num;
    background:$color
}

.div1{
    @include aa(100px,#fff)//或者写反：aa（$color:#fff,$num:100px）
}

带参数，且参数带默认值：
@mixin aa（$num,$color：#fff）{
    width:$num;
    background:$color
}


```



---





### 3.继承以及import

##### 继承

```
不带子代的：
.div1{
    width:100px;
    height:100px;
}

.div2{
    @extend .div1;
}

带子代的：
.div1{
    width:100px;
    height:100px;
    .aa{
        width:10px;
    }
}

.div2{
    @extend .div1;
}
等于
.div1, .div2{
     width:100px;
   	 height:100px;
}
.div1 .aa, .div2 .aa{
     width:10px;
}

```

##### import

```
在test.scss文件里引入公共样式common.scss

@import '.../common'

```



----





### 4.数字

##### +，-

```
.div{
    width:10px+10px;
    height:20px-10px;
}
```

##### *,/

```
.div{
    width:20px*10;//注意px，只能有一个
    
    height：（30px/10）;//注意要带括号区分关键字“/”,且px只能在除数
}
```

##### 绝对值

```
.div{
    width：abs（-10px）;
}
```

##### 函数取值

```
.div{
    width:round(5.5)px//四舍五入
    	  ceil（5.5）//向上取整
    	  floor（5.5）//向下取整
    	  percentage（30px/100px）//取百分数
    	  min（10,20,30）
    	  max（10,20,30）//最小值，最大值
    
}
```



-----



### 5.字符串

##### 字符串拼接

```
#fff + 000
得
#fff000
```

##### 大小写转换

```
to-upper-case($var);
to-lower-case($var);
```

##### 字符串长度

```
str-length($var);
```

##### 计算字符的索引

```
str-index('abc','b');//返回值为2，索引从1开始
```

##### 字符串的插入

```
str-insert('abc','d',3)//结果：abcd
```





-----



### 6.颜色

```
rgb();
rgba();//颜色参数设置

lighten($color,20%)//颜色浅20%
darken（$color,20%）//颜色深20%

opacify（$color,0.3）//更不透明0.3
transparentize（$color,0,3)//更透明0.3
```





----



### 7.列表list

##### 列表的定义

```
$icons:plus music search heart;
```



##### 返回列表长度

```
length(2px 2px 2px)//返回值为3
```

##### 返回列表索引值

```
index(1px 2px,2px)//返回结果2
```

##### 取出索引对应的值

```
nth(1px 2px,2)//返回2px
```

##### 列表元素追加

```
append（1px 2px ,3px）//返回 1px 2px 3px
```

##### 合并列表

```
join(1px 2px,3px 4px)//返回 1px 2px 3px 4px
join(1px 2px,3px 4px,comma)//返回 1px, 2px, 3px, 4px
```





-----



### 8.map(键值对)

##### map的定义

```
$color(light:#fff , dark:#000);
```

##### 获取map的值

```
$color(light:#fff , dark:#000,...);

.div{
    color:map-get($color,dark);
}
```

##### 返回所有key或value

```
$color(light:#fff , dark:#000);

map-keys($color)//返回所有key
map-values($color)//返回所有value
```

##### 判断map是否包含某个key

```
$color(light:#fff , dark:#000);

map-has-key($color,light)//
```

##### 合并map

```
$color(light:#fff , dark:#000);

map-merge($color,（gray:#ccc）)//返回$color(light:#fff , dark:#000,gray:#ccc);
```

#####  移除

```
$color(light:#fff , dark:#000);

map-remove($color,light,dark);
```





---





### 9.布尔

##### 比较运算符

```
>= ,<= ,< ,> ,==
```

##### 逻辑运算符

```
and , or , not
```





----



### 10.interpolation(#{$val})插值

#####  在注释中引用

```
$fz=font-siza;

/* #{$fz} */ //输出为 /* font-size */
```

##### 在选择器中引用

##### 在属性名中引用

```
$fz=font-siza;
.div{
    #{$fz}:12px;//即：font-size:12px;
}
```



---



### 11.数据类型

```
$val=rgb(0,0,0);

type-of（$val）;//返回值为：color
```





---



### 12.控制指令

##### if else

```
示例：与js一模一样，在关键字前加@即可
@function foo（$arg）{
    @if ($arg == 1){
        @return #000;
    }@else if($arg == 2){
        @return #fff;
    }@else{
        @return #111;
    }
}
```

##### for循环

```
$end = 12;

@for $i from 1 through 12{
    ...
}//包含12

@for $i from 1 to 12{
    ...
}//不包含12，只到11

```

##### each

```
$icons:plus music search heart;

@each $icon in $icons{
    .abc-#{$icon}{
        background:url($icon + '.png');
    }
}

结果：
.abc-plus{
     background:url(plus.png);
}
.abc-music{
     background:url(music.png);
}
.abc-search{
     background:url(search.png);
}
.abc-heart{
     background:url(heart.png);
}
```

##### while

```
$i:5;
@while $i  > 0{
    .col-md-#{$i}{
        width:percentage($i/100);
    }
    $i:$-2;
}


结果：
.col-md-5{
    width:5%;
}
.col-md-3{
    width:3%;
}
.col-md-1{
    width:1%;
}
```







### 13.函数

###### @function

```
@function 函数名(参数){
    ....函数体
}
```

##### @warn,@error 错误提示

```
@warn 'xxxxx';
@error 'xxxx';
```



