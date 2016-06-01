# learn-compass
compass  学习
compass核心模块:
Reset/Layout(页面布局控制)
CSS3/Helpers/Typography()/Utilities/Browers Support

compass核心模块中，只有reset和 layout需要显示引入，其它模块在@import "compass"时候就引入了。

@import "compass/reset"  
@import "compass/layout"  

用normalize替换compass内置的的reset：（normalize是compass的插件）

normalize改良了compass/reset ,统一了跨浏览器差异，而不是都清0；

1、安装normalize：

gem install compass-normalize  

2、引入插件：
修改config.rb文件，在文件头部添加
require 'compass-normalize'
@import "normalize"


/*************************************/

compass/import-once/activate：

一般生产的config.rb文件头部会有 require 'compass/import-once/activate'：

这个插件的作用是防止sass的 @import 多次引入重复的文件，引入这个插件后即使写多次 @import "aa",也只会引入一次aa。若确实想多次引入aa ,则应写成 @import "aa!" ，末尾添加叹号，则会多次引入。

叹号小技巧：

如果将config.rb配置文件中设置  output_style = :compressed 生成的压缩css文件中的注释会被删除，如何防止注释被删除？在注释的开头加"!"，则注释会保留，即使设置了 output_style = :compressed。

3、sass文件中用 @import "normalize"  替换 @import "compass/reset"

按需引入normalize的核心模块：

引入代码：@import "normalize-version"必须引入，后面跟需要的normalize模块

@import "normalize-version";  
/* 分割1 */   
@import "normalize/base";  
/* 分割2 */   
@import "normalize/html5";  
/* 分割3 */   
...  


按需引入compass 中 reset的核心模块
@import "compass/reset/utilities"

$base-font-size:16px;
$base-line-height:24px;

初始化HTML的字体和行高
@include establish-baseline()

body{
 @include debug-vertical-alignment()
}
垂直韵律字体
@include adjust-font-size-to(48px);

compass sprite "images/logo/*.png"
$logo-sprite-dimensions:true;(默认设置图片类名的宽和高)
$disable-magic-sprite-selectors:true;(关闭默认的active和hover的图片名字,可用自定义的)
$logo-layout :  smart;

详细参考：http://compass-style.org/reference/compass/

最后介绍一个小技巧： compass stats 命令可以统计项目的各项sass指标， 比如说mixin的定义数以及被调用的次数， 选择器数量， 样式属性数量， 文件大小等， 时常review这些指标并相应优化一定错不了。