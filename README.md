## 产品流程

### 前期准备

1. 产品画出大致原型后，与前后端负责人沟通技术实现难度

2. 产品负责人开会进行项目立项，UI前后端明确需求

3. 给产品负责人大致的工期排期。

4. 在工作室的 github 账号下建立项目的代码仓库

5. 前后端仓库分离，仓库名尽量统一为ProjectName-front ProjectName-app  ProjectName-server

6. 产品负责人负责定期询问进度

### 开发中

1. 前后端同学协作，进入开发状态

2. 接口使用 restful API 或其他风格

3. 后端把controller层以及pojo写好，要求遵循java doc(每个方法都要)注释规范，并通过smart-doc[https://github.com/smart-doc-group/smart-doc]生成api文档，将文档交给前端与前端进行沟通，沟通具体实现。

4. 开发过程认真负责，及时沟通

5. 有产品相关问题及时与产品负责人沟通。

6. 及时提交 commit，通过项目开发熟悉 git 工作流（很重要的技能）

### 部署上线

部署上线采用ci流程,具体实现为Docke+Travis-ci+Github+watchower

详细操作流程请见https://github.com/CyberspaceStudio/QingYuan-Infrastructure