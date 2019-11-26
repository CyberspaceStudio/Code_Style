# 目录结构

创建springboot项目，src代码层目录内容基本如下：

## java文件夹中：
1. controller 控制器层，用于请求处理
2. config     配置文件，用于编写配置文件
3. mapper/dao  数据访问层，用于定义mybatis或者其他数据访问接口文件
4. model 模型层，用于放置简单模型，对应数据库实体
5. dto 用于处理特定数据类型，放置视图或联合查询数据结构
6. filter 过滤器层，用户放置拦截器，过滤器
7. service 服务层，用于放置服务层接口，内含impl文件夹，用于实现服务层接口
8. util 工具类，用于放置各种工具类程序

## resources文件夹中放置：
1. mapping  mybatis映射文件
2. static 静态资源文件
3. template 当使用模板时，放置模板网页
4. application.yml springboot配置文件
5. generatorConfig.xml mybatisGenerator配置文件，上传git时请勿上传