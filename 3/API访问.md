# API访问
[1  ajax技术](#user-content-1--ajax技术)

[2  ajax.js模块](#user-content-2--ajax.js模块)

[3  dao.js模块](#user-content-3--dao.js模块)

​	

##  1  ajax技术

我们使用ajax访问后台API。

具体来说，创建`XMLHttpRequest`对象，向后台服务器发起http请求，获取服务器返回的结果。



##  2  ajax.js模块

把发起ajax请求的代码进行封装，形成一个模块，放在`src/modules/ajax.js`中。在页面中无需自己实现，直接调用`ajax.js`模块即可。

​	

下面给出一个调用`ajax.js`的例子：

```react
import ajax from './src/module/ajax.js';

let condition = {
  page: 1,
  pageSize: 10
}

ajax({
  url:'user/list',
  type: 'get',
  data: condition,
  success: function (response) {
    // response是后台返回的json    
  },
  error: function(msg){
    // msg是一个字符串，描述错误内容
  } 
})
```

引入的ajax模块是一个函数，调用函数时传入一个对象作为参数。此对象描述了本次请求的一些配置信息，具体包含以下几个配置项：

- **url**   string类型，描述请求地址


- **type**   string类型，描述请求类型，分为get、post、put、delete、file五种；其中前四种是

  RESTful规范中定义的四种http请求类型，file类型在上传文件时使用


- **data**   一般是object类型，描述了请求数据；特殊的，当`type`为file时，此字段为File类型，表示上传的文件


- **success**   函数类型，描述了当请求成功时的回调处理方法；回调函数包含一个参数response，它是从后台返回的json数据


- **error**   函数类型，描述了请求发生错误时的回调处理方法；回调函数包含一个参数msg，它是一个字符串，描述了错误信息

  ​

##  3  dao.js模块

在大多数页面中，我们会定义一个`dao.js`文件。把页面与服务器沟通的部分全部写在`dao.js`中，实现了数据获取与数据处理分离。

在外部代码中，仅从dao中获取数据，而不需要了解数据获取的具体方式。


