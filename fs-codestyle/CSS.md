#### 缩进
<b>[强制]</b> 使用4个空格作为一个缩进层级。
<b>[强制]</b> 选择器与 { 之间必须有空格
```css
.selector {

}
```
<b>[强制]</b> 属性名与后面的 : 不能有空格；: 与后面的属性值之间必须包含空格
```css
margin: 0;
```
<b>[强制]</b> 列表型属性书写在单行时， , 后面必须跟一个空格
```css
font-family: Arial, sans-serif;
```

#### 行长度
<b>[强制]</b> 每行不得超过120个字符，除非单行不可分割
> URL较长就属于不可分割的情况
<b>[强制]</b> 对于超长的样式，在样式值的 空格 处或 , 之后换行，建议按逻辑分组
```css
background:
    transparent: url(aLongLongLongLongLongURL)
    no-repeat 0 0;
```

#### 选择器
<b>[强制]</b> 当一个 rule 包含多个 selector 时，每个选择器声明必须独占一行
```css
.post,
.page,
.comment {
    //rule
}
```
<b>[强制]</b> > 、 + 、 ~ 选择器的两边必须保留一个空格
<b>[强制]</b> 属性选择器的值中必须用双引号包围
<b>[强制]</b> 属性定义必须另起一行,属性定义后面必须用分号结尾
```css
//good
.selector {
    margin: 0;
    padding: 0;
}
//bad
.selector {margin: 0; padding: 0}
```
<b>[强制]</b> 如无必要，不要使用！important 行内样式
