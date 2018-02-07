---
 title: bootstrap v4 学习笔记（2）
 date: 2018-02-06 09:17:00
 tags: bootstrap v4
 thumbnail: /images/bootstrap.jpg
 categories: study
---

 button和dropdown(2):
 一个div里加入多个button，组成按钮群，div应用btn-group类，可加入aria-label和role属性给整个btn-group定固定标签和role，group的role就是group
 div内的button应用btn 和btn-*样式类（type必须是button）

 一个按钮工具栏可以横向容纳多个btngroup或是btn，抑或两者都有

 在input内部添加按钮,可以将一个div应用input-group-text,在外包裹另一层div应用input-group-prepend class ，并把此div和 input放入一个总div内，总div应用input-group类
 input要应用form-control类，见input

 btn-group内可以定义一个下拉菜单，将整个下拉菜单定义成一个btn-group，里面包含一个控制下拉的button和一个div应用dropdown-menu class，内部包含下拉菜单的子选项：一些a或者button标签，控制button应用btn btn-* dropdown-toggle 三个class和（可选）aria-haspopup=true aria-expanded=false（无障碍），子选项需要应用dropdown-item class,此button是下拉点击一体化的

 如果要一个下拉按钮和显示按钮分开的dropdown控制按钮，则一个控制下拉的button需要分为两个button，一个仅应用btn btn-*样式class，而另一个应用btn btn-* dropdown-toggle dropdown-toggle-split class，内部包含一个class="sr-only"的span（注：原控制按钮的dropdown-toggle应用在新分离的button上）
 如果需要将弹出menu向右弹，则在btn-group class的div上加一个dropright class

 dropdown-menu内除了加子选项外，也可添加应用了dropdown-divider class的div 这样就有了子选项之间的分割线 
 子选项可以添加active类使其显示为高亮，也可添加disabled class使其禁用


 也可使用btn-group-vertical代替btn-group，这样整个btn-group就是竖直状态的 




