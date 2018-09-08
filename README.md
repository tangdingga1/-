# 精简省市区县连动下拉框
## 快速使用
1. 下载文件pro_select.js，并在页面当中引入。此时全局会产生一个名为**pro_select**的函数。
2. 使用函数pro_select，并传入一个对象(Object)作为函数的参数。就像这样  
```
pro_select({
    pro_id : 'pro',//这里填写你的省选择框id
    city_id : 'city',//这里填写你的市选择框id
    unit_id : 'unit',//这里填写你的区选择框id
    street_id : 'street'//这里填写你的县选择框id
});
```
![](./src/init.jpg '初始化效果')  
3. 如果你不需要这么多的信息。你可以使用pro_selecte.config(number)。来进行配置。比如你只需要省市两个层级，先使用pro_selecte.config(2)进行配置。然后使用pro_select函数传入id数据。此时你只需要传入两个对应的id数据，如
```
//先使用config函数
pro_selecte.config(2);
pro_select({
    pro_id : 'pro',//这里填写你的省选择框id
    city_id : 'city'//这里填写你的市选择框id
});
```
4. 如果你需要初始化省市区县被选中的状态，那么可以在传入pro_select函数对象中加上初始化数值数据。
```
pro_select({
    pro_id : 'pro',
    city_id : 'city',
    unit_id : 'unit',
    street_id : 'street',
    pro_v : '四川',
    city_v : '成都',
    unit_v : '温江区',
    street_v : '金马镇'
});
```
值可以不完整。比如只传一个省，那么市区县会自动初始化为默认的第一个。但是不能隔级传值，比如传一个省和一个区。
**如果数据初始化不出来，直接去JS文件里面用你的省市区名查找下，看是不是少了多了个字，按照自己的需求修改一下。**
## 省市区县下拉框微信小程序组件版
因为工作要求省市区县，但是微信小程序只有省市区的自带组件。所以写了一个多连级的省市区的自定义组件，在location_options。如果需要可以拿去。  
使用时，只需要按照微信小程序自定义组件的使用方法，在要使用的page页面json文件中传入组件路径和组件名。然后再页面中直接使用就好了。
```
{

    "usingComponents": {
        "Location": "location_options/location_options"
    }
}
//wxml中使用
<Location bind:myevent="{{}}" pro="{{}}" city="{{}}" unit="{{}}" street="{{}}"></Location>
```
![](./src/wechat.png '初始化效果')  
其中组件上面你可以传入自己需要的初始化的默认值。
- pro 代表默认省
- city 默认市
- unit 默认区
- street 默认街道  
- bind:myevent 传入点击确定之后你继续操作的事件名称。在page页面的js文件中，使用e.detail得到用户选择的省市区县街道**数组**。之后你可以继续操作。  

**如果你需要在一个页面使用两次组件，记得传入两个，使用两个组件名。不然内部data数据会影响到另一个组件**
## P.S.
- 写的初衷是因为网上这方面的工具集大多复杂纷繁华而不实。其次公司使用的前端技术很老旧，框架用的还是几年前的layui，事件一下子就会被覆盖掉。所以写了一个简单的连动。
- 我个人认为前端工程师应该是简洁而又优雅的。所以轮子也好框架首先应该是简单易改的，写出来逻辑，更多是自定义的修改和可塑性。所以想尝试写一下单纯脱离样式的逻辑性的工具。
- 最后我想说，在搬砖的阶段，远离使用非mvvm框架前端架构落后的公司，真的是保自身时间平安。想想同样的时间，我react真的能写layui两倍的页面。在工程化的协作下，还用页面去分层，用一个个函数，jq去操作DOM。维护起来真的会死人的。
