# 如何解决IE兼容性问题

所谓的浏览器兼容性问题，是指因为不同的浏览器对同一段代码有不同的解析，造成页面显示效果不统一的情况，在大多数情况下，我们的需求是，无论用户用什么浏览器来查看我们的网站或者登陆我们的系统，都应该是统一的显示效果。随着浏览器版本的增多，解决IE浏览器兼容性显得尤为重要. 

一、!important (功能有限)   
随着IE7对!important的支持, !important 方法现在只针对IE6的兼容.(注意写法.记得该声明位置需要提前.)   
例如: 
  ```
  #example {    
              width: 100px !important; /* IE7+FF */   
              width: 200px; /* IE6 */   } 
  ```
二、css HACK的方法

所有浏览器 通用 height: 100px;   
IE6 专用 _height: 100px;   
IE7 专用 *+height: 100px;   
IE6、IE7 共用 *height: 100px;    
IE7、FF 共用 height: 100px !important; 

需要注意的是，代码的顺序一定不能颠倒了，要不又前功尽弃了。因为浏览器在解释程序的时候，如果重名的话，会用后面的覆盖前面的，就象给变量赋值一个道理，所以我们把通用的放前面，越专用的越放后面 解释一下4的代码：  
  读代码的时候，第一行height:100px; 大家都通用，IE6 IE7 FF 都显示100px    
  到了第二行*height:300px; FF不认识这个属性，IE6 IE7都认，所以FF还显示100px，而IE6 IE7把第一行得到的height属性给覆盖了，都显示300px     到了第三行_height:200px;只有IE6认识，所以IE6就又覆盖了在第二行得到的height,最终显示200px     
注意：
  *+html 对IE7的兼容 必须保证HTML顶部有如下声明：    〈!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"     "http://www.w3.org/TR/html4/loose.dtd"〉
