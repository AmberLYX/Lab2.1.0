Lab 3 : Persistence Ignorance
===================================

Introduction  
--------------------------------------  

成员信息：

[刘奕秀]- 201931990209 - 1978933929@qq.com (TECH LEAD)

[李敏]- 201931990403 - 2609891867@qq.com


1. 了解存储库的模式。  

2. 了解服务层模式。  

3. 理解为什么将业务逻辑与数据存储技术分离起来很重要  

Material and Methods  
-----------------------------------  

2.1 工具
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Repository Pattern：

在域和数据映射层之间添加仓储层，以将域对象与数据库访问代码的细节隔离开来，并最小化查询代码的分散和重复。

2.2 方法
~~~~~~~~~~~~~~~~~~~~~~~~~~~

存储库模式 ：

https://www.cosmicpython.com/book/chapter_02_repository.html 

Result  
-----------------------------------------  

3.1 repository.py 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**代码** 

.. code::  

 import abc
 import model
 import os,pickle


 class AbstractRepository(abc.ABC):
    @abc.abstractmethod
    def add(self, batch: model.Batch):
        raise NotImplementedError

    @abc.abstractmethod
    def get(self, reference) -> model.Batch:
        raise NotImplementedError


 class SqlAlchemyRepository(AbstractRepository):  
    def __init__(self, session):
        self.session = session

    def add(self, batch):
        self.session.add(batch)

    def get(self, reference):
        return self.session.query(model.Batch).filter_by(reference=reference).one()

    def list(self):
        return self.session.query(model.Batch).all()

 class PickleRepository(AbstractRepository):
    ''' Complete the definition of this class. '''
    def __init__(self, path = None):
        self.path = path

    def add(self, batch):
        f = open(self.path, 'wb')   #以二进制格式写入文件
        pickle.dump(batch, f)       #将 Python 中的对象序列化成二进制对象，并写入文件
        f.close()

    def get(self, reference):
        result = []
        batches = list(self.path)   #获取pickle文件中所有Batch对象
        if batches:
            for batch in batches:
                if batch.reference == reference:  #查找所有符合对象
                    result.append(batch)     
        return result

    def list(self):
        if os.path.getsize(self.path) > 0:  #判断文件是否为空
            f = open(self.path, 'rb')       #以二进制格式读取文件
            batches = []
            while 1:        #读取未知数量的 pickle 对象，反复 load 文件对象，直到抛出异常为止
                try:
                    batches.append(pickle.load(f))  #读取指定的序列化数据文件，并返回对象
                except EOFError:
                    break
            f.close()
            return batches

3.2 运行结果
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. image:: ../../media/测试结果.png

3.3 视频结果
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

【测试过程.mp4】  https://cloud.zjnu.edu.cn/share/5eaf2b5a0d73b72ca063fd3583

Discussion
-----------------------------------
1. 教科书test services.py和我的test services.py有什么区别？

答：读取数据的来源不同。旧的 services.py 使用 SqlAlchemy 将数据存入 session 中再与 PostgreSQL 进行数据交互，新的 services.py
使用 pickle 调用定义方法将数据转换为二进制格式存储到.pickle 文件中

2. 在我们选择为存储库模式使用另一个实现后，服务层是否受到了影响？我们可以说服务层不知道持久性吗？

答：1.选择为存储库模式使用另一个实现后，服务层不会收到影响。业务逻辑层会调用数据持久层的逻辑来访问数据库，在本次实验中即使将原本对数据库的操作改为 pickle，实际上仍然是对数据的操作。
    2.我们可以说服务层不知道持久性。
  
3. 将业务逻辑与基础设施问题分离有什么好处？

答：耦合度的降低，使得代码的重用率更高。
 
4. 在哪里定义了业务逻辑，以及在哪里定义了基础结构？告诉我Python文件名.

答：在model.py定义了业务逻辑， repository.py中定义了基础结构

Reference
-------------------------------------

[1]https://blog.csdn.net/weixin_42072280/article/details/105989561

[2]http://c.biancheng.net/view/5736.html

[3]https://blog.csdn.net/weixin_34362875/article/details/89770393



