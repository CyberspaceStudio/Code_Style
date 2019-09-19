1. 文件
<b>[强制]</b>在文件结尾处保留一个空行

2. 结构
2.1 缩进
<b>[强制]</b>使用<b>4</b>空格做为一个缩进层级
<b>[强制]</b>switch下的case和default必须增加一个缩进层级
```
switch (variable) {

    case '1':
        //do...
        break;

    case '2':
        //do...
        break;
    
    default:
        //do...

}
```

2.2 空格
<b>[强制]</b>二元运算符两侧必须有一个空格，一元运算符域操作对象之间不允许有空格
```
const a = !arr.length;
a++;
a = b + c;
```
<b>[强制]</b>用作代码块起始的左花括号{前必须有空格
```
if (condition) {

}
while (condition) {

}
function funcName() {

}
```
<b>[强制]</b>在函数调用、函数声明、括号表达式、属性访问、if / for / while / switch / catch 等语句中,()和[]内紧贴括号部分不允许有空格
```
//good
if (condition) {

}
//bad
if ( condition ) {

}
```
<b>[强制]</b>单行声明的数组和对象,如果包含元素，{}和[]内紧贴括号部分不允许包含空格
<b>[强制]</b>行尾不得有多余的空格

2.3 换行
<b>[强制]</b>每个独立语句结束后必须换行
<b>[强制]</b>每行不得超过120个字符
> 超长不可分割逻辑，复杂正则表达式，长字符串可不遵守

<b>[强制]</b>运算符处换行，运算符必须在新行的行首
```
if (user.isAuthorize()
    && user.isInRole('admin)
    || user.hasCookie()
) {
    //do
}
```
<b>[强制]</b>在函数生命、函数表达式、函数调用、对象创建、数组创建、for 语句场景中，不允许在 , 或 ; 前换行
```
//good
const obj = {
    a: 1,
    b: 2,
    c: 3
}
//bad
const obj = {
    a: 1
    ,b: 2
    ,c: 3
}
```
<b>[建议]</b>不同行为或逻辑的语句集，使用空行隔开，更易阅读
<b>[建议]</b>在语句的行长度超过120时，根据逻辑条件合理进行缩进
```
const html=''   //使用空字符串便于后面html字符串严格缩进
        + '<div>'
            + '<span></span>'
            + '<span></span>'
        + '</div>'

{
    openState
        ? children
        : null
}
```
> 强烈建议将逻辑判断前置，净化condition

```
//good
const isAdmin = getUserRole();
const userArticleNum = getUserArticles()
if (isAdmin && userArticleNum) {
    //do
}
//bad
if (getUserRole() && getUserArticles()) {
    //do
}
```
<b>[建议]</b>对于 if...else... 、 try...catch....finally 等语句，推荐使用在}后添加一个换行的风格。
```
if (condition) {
    //do
}
else {
    //do
}

try {
    //do
}
catch (ex) {
    //do
}
```

2.4 语句
<b>[强制]</b>不得省略行尾后的空格
<b>[强制]</b>在 if / else /for / do / while 中，即使只有一行，也不能省略{...}
<b>[强制]</b>函数定义结束不得添加分号
<b>[强制]</b>IIFE必须在函数表达式外添加( , 非IIFE不得在函数表达式外添加(
```
//good
const task = (function () {
    //code
    return res;
})()
const func = function () {

}
//bad
const task = function () {
    //code
    return res;
}()
const func = (function () {})
```
3.命名
<b>[强制]</b>变量，函数命名，函数的参数使用Camel命名法
```
const loadingModal = ''
function loadingModal(loadingState) {
    //do
}
```
<b>[强制]</b>常量使用全部字母大写，单词间下划线分隔的命名方式
```
const HTML_EMTITY = ''
```
<b>[强制]</b>类使用PasCal命名法
```
class TextNode {
    //do
}
function TextNode(options) {
    //do
}
```
<b>[强制]</b>类的方法/属性使用Camel命名法
<b>[强制]</b>枚举变量使用Pascal命名法，使用全部字母大写，单词间下划线分隔的命名方式
```
const TargetState = {
    READING: 1,
    READY: 2
}
```
<b>[强制]</b>类名使用名词(OOP)
<b>[建议]</b>boolean类型的变量使用 is 或 has 开头

4. 注释
4.1 单行注释
<b>[强制]</b>必须独占一行， // 后跟一个空格
4.2 多行注释
<b>[建议]</b>避免出现/*...*/这样的多行注释。有多行注释内容时，使用多个单行注释
4.3 文件注释
```
/**
 * @file describle the file 
 * @author ...
 */
```
4.4 常量注释
```
/**
 * @const 
 * @type {string}
 */
```
4.5 细节注释
> 对于内部实现，不易理解的逻辑说明、摘要信息等，可能需要写细节上注释
<b>[建议]</b>细节注释遵循单行注释的标准。说明必须换行时，每行是一个单行注释的开始
```
function foo(p1, p2) {
    // ...
    // ...
}
```
5. 语言特性
5.1 变量
<b>[强制]</b>变量声明前必须先定义
<b>[建议]</b>原则上我们取消一切 var 声明变量的场景，根据场景自行选择 let const 进行变量声明
<b>[强制]</b>变量必须 <b>即用即声明</b>,不得在函数或其他形式的代码块起始位置统一声明所有变量
5.2 条件
<b>[强制]</b>避免在任何场景下使用 == ,应全部使用 === ,仅在判断 null == undefined时允许使用
<b>[建议]</b>通常情况下你的表达式都应该做review，让他更加精简
<b>[建议]</b>按执行频率排列分支的顺序
<b>[建议]</b>对于使用变量或者表达式的多值条件，用 switch 代替 if
<b>[建议]</b>如果函数或全局中的 else 块后没有任何语句，可以删除 else
```
//good
function getName() {
    if (name) {
        return name;
    }

    return 'unnamed';
}
//bad
function getName() {
    if (name) {
        return name;
    }
    else {
        return 'unnamed';
    }
}
```
5.3 循环
<b>[建议]</b>不要在循环体中包含函数表达式，事先将函数提取到循环体外
<b>[建议]</b>对循环体外多次使用的不变值，在循环外用变量缓存
<b>[建议]</b>对有序集合进行遍历时，缓存length
> 虽然现代浏览器都对数组长度进行了缓存，但对于一些宿主对象和老旧浏览器的数组对象，每次在length访问时动态计算元素个数，缓存此时length能有效值提高程序性能
```
for (let i = 0, len = elements.length; i < len; i++) {
    const element = elements[i];
    //do
}
```
5.4 类型
<b>[建议]</b>类型检测优先使用typeof。对象类型检测使用instaceof。null或undefined的检测使用 == null
<b>[建议]</b>转换成string时，使用 + ''
<b>[建议]</b>转换成number时，通常使用 +
<b>[建议]</b>string转换成number，要转换的字符串结尾包含非数字并期望忽略时，使用parseInt
```
const width = '200px'
parseInt(width, 10)
```
<b>[强制]</b>转换成boolean时，使用 !! ,避免依赖内置隐式类型转换
<b>[建议]</b>使用parseInt时必须指定进制
```
//good
parseInt(str, 10);
//bad
parseInt(str);
```
5.5 字符串
<b>[强制]</b>字符串的开头和结束用单引号 '
5.6 对象
<b>[强制]</b>使用对象字面量 {} 创建对象。
<b>[建议]</b>对象创建时，对于对象的属性是否加引号的行为保持一致
<b>[强制]</b>不允许修改和扩展任何原生对象和宿主对象的原型
```
String.prototype.trim = function () {

}
```
5.7 数组
<b>[强制]</b>使用数组字面量 [] 创建新数组，除非想要创建指定长度的数组
<b>[强制]</b>遍历数组不用 for in 
> 数组对象可能存在数字以外的属性

<b>[建议]</b>清空数组使用 .length = 0
5.8 函数
<b>[建议]</b>一个函数的长度控制在 50 行以内
> 大多数情况下你的函数逻辑都可以得到较好的拆分
  一些函数式编程的东西或许你需要知道

<b>[建议]</b>一个函数的参数长度控制在 6 个以内
<b>[建议]</b>非输入性参数使用 options 进行传递
> 避免出现 func(a, true, false, true, true)之类很难明确的参数传递
```
//good
function checkElement(element, {isAdmin: true, isCookieValid: false}) {
    if (options.isAdmin) {
        //do
        element...
    }
    if (options.isCookieValid) {
        //do
    }
}
//bad
function checkElement(element, isAdmin, isCookisValid) {
    if (isAdmin) {
        //do
        element...
    }
    if (isCookieValid) {
        //do
    }
}
```
<b>[建议]</b>空函数不使用 new Function() 的形式
<b>[建议]</b>对于性能有要求的场合，建议存在一个空函数的常量，供多处使用共享
```
const EMPTY_FUNCTION = function () {}
```
5.9 面向对象
<b>[强制]</b>类的继承方案，实现时需要修正 constructor
<b>[建议]</b>声明类时，保证 constructor 的正确性
```
function Animal(name) {
    //do
}
// 直接指向新对象需要修正
Animal.prototype = {
    constructor: Animal,
    jump: function () {}
}
// 此时不需要
Animal.prototype.jump = function() {
    //do
}
```
> 除此之外，我们希望你理解 es6 的 class 语法

<b>[建议]</b>属性在构造函数中声明，方法在原型中声明
<b>[强制]</b>自定义事件全部使用小写字母
<b>[强制]</b>设计自定义事件时，应考虑禁止默认行为
> 常见禁止默认行为的方式
> 1. 事件监听函数中 return false
> 2. 事件对象中包含禁止默认行为的方法， 如preventDefault

5.10 动态属性
<b>[强制]</b>避免直接使用 eval 函数
<b>[强制]</b>禁止使用 with 函数
<b>[建议]</b>减少 delete 的使用
> 在严格模式或者IE下使用 delete 时，不能删除的属性将会引发报错

5.11 对象属性
<b>[建议]</b>避免直接修改传入的对象
> 你应该清除这会导致函数外部对象的状态， 你可以使用deepClone代替