Lab 2 Handout: Using Blueprints to Architect A Photo Album Web Application   
===================================

Introduction
----
+ 下载Photo String的源代码并运行。

+ 绘制以下蓝图：upload_bp, show_bp, search_bp, and api_bp

+ 将上述蓝图注册到web应用程序。

+ upload_bp允许上传新照片，关联的路由为/upload。

+ show_bp允许按时间顺序显示所有照片及其描述,关联的路由为/show。

+ search_bp允许根据照片描述过滤照片，关联的路由为/search/query-string（返回描述与查询字符串匹配的照片作为搜索结果）。

+ api_bp允许从命令行获取JSON格式的所有照片信息，关联的路由是/api/json（返回的json字符串必须包含每张照片的照片ID、上载日期、照片大小（KB）和照片描述）。

+ 添加新功能

**Lumache** (/lu'make/) is a Python library for cooks and food lovers
that creates recipes mixing random ingredients.
It pulls data from the `Open Food Facts database <https://world.openfoodfacts.org/>`_
and offers a *simple* and *intuitive* API.

Check out the :doc:`usage` section for further information, including
how to :ref:`installation` the project.

.. note::

   This project is under active development.

Contents
--------

.. toctree::

   usage
   api
