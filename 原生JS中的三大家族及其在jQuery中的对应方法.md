# 原生JS中的三大家族：offset/scroll/client

## JS中的offset家族:

**一、offsetWidth与offsetHeight：**  console.log(box.offsetWidth);

获取的是元素的实际宽高 = width + border + padding

注意点： 

1.可以获取行内样式表及内嵌样式的宽高 
2.获取到的值是一个number类型，不带单位 
3.获取的宽高包含border和padding 
4.只能读取，不能设置

![images](https://github.com/sunidol/JavaScript/blob/JavaScript-journal/images/1.png)

**二、offsetLeft与offsetTop：**

offsetLeft:获取自己左外边框与offsetParent的左内边框的距离

offsetTop:获取自己上外边框与offsetParent的上内边框的距离

![images](https://github.com/sunidol/JavaScript/blob/JavaScript-journal/images/2.png)

**三、offsetParent:**

获取最近的定位父元素 （自己定位参照的父元素）

注意点： 

1.如果元素自身是固定定位（fixed），则定位父级是null 
2.如果元素自身是非固定定位,并且所有的父元素都没有定位，那么他的定位父级是body 
3.body的定位父级是null

## jQuery中获取宽高的方法:

**一、width()/height()方法:**

获取到的是内容的宽高，即width/height

注意点： 

1.获取到的就是内容的宽高,不带px的number类型的值. 
2.获取不传参 
3.传参代表的是设置内容的宽高

//例子：模拟响应式布局.

      $(window).on('resize', function () {
        if($(this).width() > 1200){
          $('body').css('backgroundColor','red');
        }else if($(this).width() > 900){
          $('body').css('backgroundColor','yellow');
        }
        else if($(this).width() > 600){
          $('body').css('backgroundColor','pink');
        }else if($(this).width() > 400){
          $('body').css('backgroundColor','green');
        }else {
          $('body').css('backgroundColor','white');
        }
      });
      
**二、innerWidth()/innerHeight()方法：**

获取到的是内容的宽高+padding 

注意点： 

1.获取到的就是内容+padding的宽高,不带px的number类型的值
2.获取不传参 
3.传参代表的是设置内容的宽高，但是注意这里不会改变border的大小

**三、outerWidth()/outerHeight()方法：**

获取到的是内容+padding+border+margin 的宽高

注意点： 

1.获取到的是内容+padding+border+margin 的宽高
2.不传参代表的是获取获取到的是内容+padding+border 的宽高
3.传的参数是true，获取到的是内容+padding+border+margin 的宽高

**四、获取页面可视区的宽高**

1、宽度：$(window).width()

2、高度：$(window).height()

**五、offset()方法：获取到的是一个对象,里面有left值和top的值**

注意点：

1.offset()方法获取到的是一个对象,里面有left值和top的值. 
2.offset方法获取元素距离document的位置. 
3.不传参是获取，传参是设置

//设置,设置的时候给一个包含了left和top属性的对象.
        $('#son').offset({
          left:200,
          top:200
        });
        
## JS中的scroll家族   

**一、scrollwidth与scrollHeight:**

获取元素内容的真实宽高，这里是内容，不包括内边距以及border

1、scrollHeight表示元素的总高度，包括由于溢出而无法展示在网页的不可见部分

2、scrollWidth表示元素的总宽度，包括由于溢出而无法展示在网页的不可见部分

3、scrollTop：onscroll事件发生时，元素向上卷曲出去的距离

4、scrollLeft：onscroll事件发生时，元素向左卷曲出去的距离



## jQuery中scrollTop()与scrollLeft()方法

jQuery中的scrollLeft与scrollTop的方法和原生的js的一样。

1、获取页面被卷曲的高度 $(window).scrollTop();

2、获取页面被卷曲的宽度 $(window).scrollLeft();

## JS中的client家族

1、clientWidth/clientHeight：获取可视区域的宽高

2、clientTop/clientLeft:不常用，其实就是左边框border-left和上边框border-top

原生获取可视区域的clientHeight与clientWidth的方法：

//封装浏览器兼容函数获取界面可视区域

    getClientSize = function (  ) {
        return {
            clientWidth : window.innerWidth || document.documentElement.clientWidth || document.body.clientWidth || 0,
            clientHeight : window.innerHeight || document.documentElement.clientHeight || document.body.clientHeight || 0,
    }
    
## jQuery中的position()方法

position方法：获取的是元素距离有定位的父元素(offsetParent)的位置

注意点： 

1.获取到的也是一个对象,包含top和left值. 
2.不能进行设置

$('#btn2').on('click', function () {
        //获取
        console.log($('#son').position());


        //不能设置
        // $('#son').position({
        //   left:200,
        //   top:200
        // });
      });
      
# 总结： 

### 相同点： 

a、js中的scrollLeft与scrollTop与jQuery中的一样 

b、js中的offsetLeft及offsetTop和jQuery中position方法一样 

c、 $(window).width() 
$(window).height()和原生中的clientHeight与clientWidth获取可视区的宽高一致

### 最后一点，一定要理解清楚：

可视区域就是：你可以看到的区域。

浏览器窗口显示网页的部分（即不包括地址栏、工具栏）就是可视区。。

你可以用鼠标来推动浏览器窗口来改变大小，此时可视区的大小也是跟着变的。
