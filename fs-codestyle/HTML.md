#### 缩进与换行
<b>[强制]</b> 使用4个空格作为一个缩进层级
> script, style使用相同的缩进风格
```html
<style>
ul {
    color: red;
}
</style>

<ul>
    <li></li>
</ul>

<script>
// 首级代码与<script>标签同级
console.log('do')
</script>
```
<b>[建议]</b> 每行代码不超过120个字符
<b>[强制]</b> class 单词全字母小写，单词间以 - 分隔
```css
.title-error {

}
```
<b>[强制]</b> class必须代表相应模块或部件的内容或功能，不得以样式信息进行命名
```html
//good 
<div class="sidebar"></div>
//bad
<div class="left"></div>
```
<b>[强制]</b> 元素id必须保证页面唯一
<b>[建议]</b> id 建议全字母小写，单词以 - 分隔。同项目必须保持风格一致
<b>[建议]</b> 不将id用于css选择器
> id选择器命中的节点只能存在一个，用于样式容易引起错误

<b>[建议]</b> id, class在保证不冲突的情况下尽可能简短

#### 标签名
<b>[强制]</b> 标签名使用小写字母
<b>[强制]</b> 对于无需自闭合的标签， 不允许自闭合
> 常见的有 input br img hr等
<b>[强制]</b> 对HTML5中规定允许省略的闭合标签，不允许省略闭合标签
```html
//good
<ul>
    <li>abc</li>
    <li>li</li>
</ul>
//bad
<ul>
    <li>abc
    <li>li
</ul>
```
<b>[建议]</b> 在css代价较低可以实现的场景下禁止使用表格布局
> 这样将会避免很多在回流时由 table 引起的性能消耗

<b>[建议]</b> 标签的使用尽量简洁，减少不必要的标签
<b>[强制]</b> 除非你工作在要求自闭合空白标签的项目下，否则像下面这样闭合标签，这样会引起错误
```html
<div/>
<span></span>
```

#### 属性
<b>[强制]</b> 属性名使用小写字母
<b>[强制]</b> 属性值必须使用双括号包围
<b>[强制]</b> 属性名与属性值之间不允许存在空格
<b>[强制]</b> 布尔类型的属性不建议指定值
> 尽管这并不会引起错误
```html
//good
<input type="test" required>
//bad
<input type="test" required="true">
```
<b>[建议]</b> 自定义属性使用 xxx- 为前缀， 推荐使用 data-
```html
<ol data-ui-type="Select"></ol>

