## 产品流程

### 前期准备

1. 产品画出大致原型后，与前后端负责人沟通技术实现难度

2. 产品负责人(即为项目负责人)开会进行项目立项，UI前后端明确需求

3. 给产品负责人大致的工期排期。

4. 在工作室的 github 账号下建立项目的代码仓库

5. 前后端仓库分离，仓库名尽量统一为ProjectName-front ProjectName-app  ProjectName-server

6. 项目负责人负责定期询问进度

### 开发中

1. 开发过程认真负责,及时沟通

2. 有产品相关问题及时与产品负责人沟通,坚决不能出现未和产品沟通私自改需求实现的情况.

3. 及时提交 commit,通过项目开发熟悉 git 工作流

4. 前后端应保证在测试完成后再提交代码

后端具体规范请见仓库中的`server/readme.md`

### 部署上线

部署上线采用ci流程,具体实现为Docke+Travis-ci+Github+watchower

详细操作流程请见 https://github.com/CyberspaceStudio/QingYuan-Infrastructure/tree/master/server/ci

