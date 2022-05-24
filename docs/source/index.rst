Lab 2 Handout: Using Blueprints to Architect A Photo Album Web Application   
===================================


Introduction
------------------------

成员信息：

[刘奕秀]- 201931990209 - 1978933929@qq.com (TECH LEAD)

[李敏]- 201931990403 - 2609891867@qq.com

[吴佩媛]- 201931990410 - 29723741292@qq.com

  

+ 下载Photo String的源代码并运行。

+ 绘制以下蓝图：upload_bp, show_bp, search_bp, and api_bp

+ 将上述蓝图注册到web应用程序。

+ upload_bp允许上传新照片，关联的路由为/upload。

+ show_bp允许按时间顺序显示所有照片及其描述,关联的路由为/show。

+ search_bp允许根据照片描述过滤照片，关联的路由为/search/query-string（返回描述与查询字符串匹配的照片作为搜索结果）。

+ api_bp允许从命令行获取JSON格式的所有照片信息，关联的路由是/api/json（返回的json字符串必须包含每张照片的照片ID、上载日期、照片大小（KB）和照片描述）。

+ 添加新功能


Materials and Methods
------------------------

工具
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- **blueprint**：蓝图是应用中可以作为子路由的对象。蓝图定义了同样的添加路由的方式，可以将一系列路由注册到蓝图上而不是直接注册到应用上，然后再以可插拔的方式将蓝图注册到到应用程序。


方法
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

使用blueprint的方法

https://www.imooc.com/wiki/flasklesson/blueprint.html

Results
-------------

Photo String 的运行
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. image:: ../run.jpg
   :align: center
   :alt: 运行结果图


