#### URI
1. 不适用动词(行为)
> 动作操作应使用 GET, POST, DELETE, PATCH, PUT等http方法来体现

2. 使用名词
> URI[统一资源标识符]

3. 使用复数
> Notice

```javascript
//bad
/blogs/123/post
/blogs/123/post/123/comments

//good
/blogs/123/posts
/blogs/123/posts/123/comments
```

4. 不适用修饰词
> item  list entities  到底哪个合适，好像都能用,用哪个 好像同一个人来设计都会不一样！！！
```javascript
//bad
/usersList
/tagItems
//good
/users
/tags
```

#### Request Method && Response Status

1. 增
> POST  -->  201 Created

2. 删
> DELETE  -->  204 No Content

3. 替
> PUT  -->  200 Ok

4. 改
> PATCH  -->  200 OK

5. 查
> GET  -->  200 OK

#### Response Body 

> notice  这里应该还要在商量，看工作室具体能落实到什么地步

> 如果要做api文档维护的话  建议 swagger + ajv

```javascript
//schema

{
    code: {
        type: "status code",
    },
    msg: {
        type: "string",
    },
    data: {
        type: "object"
    }
}
