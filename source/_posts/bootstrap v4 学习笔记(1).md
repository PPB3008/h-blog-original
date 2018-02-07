---
title: bootstrap v4 学习笔记(1).
date: 2018-02-05 10:33:00
tags: bootstrap v4
thumbnail: /images/bootstrap.jpg
categories: study
---
#bootstrap在css和sass中的媒体查询
css中直接使用@media(max/min-width){...}作用 max/min width需自己定义
也可定义@media(max/min-width)and(max/min-width){...}，自定两种尺寸之间的动作
sass中使用mixin写法
@include media-breakpoint-up/down/only(xs/sm/md/lg){...} viewpoint尺寸处于bootstrap4种尺寸之上，之下或正好时的函数 
也可@include media-breakpoint-between(xs/...,sm/...){...}指定两种尺寸中间（单一不包括其他的尺寸）的函数



#grid布局系统
container为所有bootstrap元素的容器，宽度一般占viewpoint的70-80%，container-fluid代替container则直接占100%宽度
col-*-auto直接设置当前情况下此col所占的列数占满整个container 并可响应式 
每个col由本体和默认左右共30px的padding组成（一边15px）叫做gutter row的gutter是margin  
要除去gutter可以将所有row和col都应用上margin/padding-left/right=0的类

small medium largr extralargr对应的container的最大尺寸分别是540 720 960 1140px 他们的最大响应式viewpoint大小为576 768 992 1200px  一旦viewpoint低于一种col的最大值，此col立刻切换至其最大值对应的尺寸的响应状态
col如果不规定任何值，单单class=“col” 则这些col默认平均分配除去已规定col值之外的空间

order系统对只定义了order类的col有效 没有定义的仍然在原位 
同一个row定义col数超过12 则最后一个超过12的col和下一行的col待在一起
w-100 class:中断一个row的排列 重新起步

可通过在row内使用align-items-*定义row在container中的垂直位置，在col内使用align-self-*确定col在row内的垂直位置 
同理，可在row中使用justify-content-*达成col的flex效果  

offset偏移:调整左侧margin 依然以col为单位 offset-6：向右便宜6个单位
可直接设置ml(margin-left),mr(同)-*,auto则根据本row具体col个数和设置了ml/mr值的col的个数来决定,如两个col-4，此row剩余4个col，若两个col-4都设置了ml-auto，则每一个col-4的ml均为2，即每个ml均往右侧偏移2个col

v4可以nesting，即一个col仍可包含row，包含的row以此col的宽度再定义12列

sass可通过mixins直接在自定义的类里生产row和col
#// Creates a wrapper for a series of columns
#@include make-row();

#// Make the element grid-ready (applying everything but the width)
#@include make-col-ready();
#@include make-col($size, $columns: $grid-columns);

#// Get fancy by offsetting, or changing the sort order
#@include make-col-offset($size, $columns: $grid-columns);
如一个div 类为t1 可写成ti{
    width:800px;
    @include make-container();
} 
即可生成


sass里可以改变默认col数 默认gutter宽度 viewpoint的改变大小 container最大宽度
$grid-columns: * !default
$grid-gutter-width:* !default
$grid-breakpoints:(xs:*,sm:*,md:*,lg:*)
$grid-max-width:(sm:*,md:*,lg:*)

#media类型的封装
media class 元素里的简介图片标题 正文遵循左，右上，右下的形式,dom里从上到下排列
media-body class为标题正文 

也可用ul-li直接定义有多个media元素的列表,
ul应用list-unstyled
my mb mt mr（？）
media元素也可应用flex，如justify-content等 
media也可nesting

#content

 #content reboot
 部分标签reboot了 
 h p标签的margin-bottom分别被设置为.5rem和1rem
 ul margin-bottom 为.5rem
 nested ul没有margin-bottom
 
 dt设置为粗体,margin-left为0，bottom为.5rem
 
 form内部
 input style重设 margin和line-height设置为了inherit
 label设为 inline-block
 
 可以直接在标签末尾加入hidden属性  如<input type="text" hidden>  效果相当于css中定义 diplay:none !important;
 
 #标签
 p标签可直接应用h1-h6 class来直接变成h1-h6效果 

class display-1-4 定义大而显眼的block
lead class 将段落提出来

ul可定义list-unstyled class去除原style
也可定义list-inline和list-inline-item class变为inlineblock list


 #code

 #图片
 img标签可应用class img-fluid 将图片height:auto和max-width:100%
 img-thumbnail应用一条1px的boder
 rounded class使图片围绕在此图片同级的dom边 用float-left/right class定义左右 
 picture标签的需要在picture内的img标签定义以上style

 #表格
 
 #注释
 若要在图片下面加一小串注释 可以使用figcaption标签 图片加上figure-img class figcaption加上figure-caption class，即可在图片下插入小字注释 
 加上text-right/left类可使注释左右移动  

#组件
 alert:
 alert alert-primary/secondary/success/danger/warning/info/light/dark role=alert
 alert内如果要插入链接，需在链接应用alert-link class
 如果需要加入可取消/关闭的alert，需在alert所在元素应用alert-dismissible给close按钮留空间 close按钮应用close class 并要添加data-dismiss="alert"属性用来触发点击后的js方法（1）
 close button内部必须有元素，如添加一个aria-hidden为true，隐藏的span，否则整个close不会显示 
 在alert内加入fade和show class可以在点击close后先有消失的动画效果再从dom中移除
 js中使用jq写$(.'alert').alert('close')可以使（1）处定义过属性的alert，绑定点击close关闭的事件
 close按钮一定要用button标签写
 可使用$('myAlert').on('closed.bs.alert',function(){})自定义关闭后发生的事
 可在alert内自定义编辑内容，如可给alert添加一个h标题并应用alert-heading类，使其成为alert用标题

 badges：
 badges badges-primary/secondary/success/danger/warning/info/light/dark
 用于插入元素内小标签（如有新消息的new标签，有新更新的数字标签等）
 单独写一个span写在元素内
 为了防止用户或开发者分不清此badges具体表达的是什么（如更新还是消息）可在badges后面写一个span class="sr-only" 此span内写badges具体表达什么  
 可加一个badge-pill class 使此badge边角更圆
 也可在a标签加badge 

breadcrumb
可选标签 一般用在表单选项上  例子：home/library/data 
一般用于nav标签 nav标签内写aria-label
nav标签内用ol=>li ol使用breadcrumb class li使用breadcrumb-item class
使用active class使选项可用  

button(1)：
btn-primary/secondary/success/danger/warning/info/light/dark  实心
btn-outline-primary/secondary/success/danger/warning/info/light/dark 空心

btn-lg/btn-sm 更大/更小的按钮 
btn-block占满父级元素宽度的块级按钮  

active class确认按钮可用  默认按下按钮后颜色会变化 aria-pressed="true" 属性可以消除此变化  使按钮一直颜色一直处于被按住的状态 
在button标签最后加disabled可使button禁用

如果使用a标签做按钮，则不支持disabled属性 可以通过添加disabled类来达到相同效果  
data-toggle="button"属性使按钮点击切换状态 按一下后一直显示按住状态，再按一下之后一直显示未按状态 


