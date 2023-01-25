# ES6-ES13新特性

# ECMA新描述概念

## 新的ECMA代码执行描述

◼ **在执行学习JavaScript代码执行过程中，我们学习了很多ECMA文档的术语：** 

 执行上下文栈：Execution Context Stack，用于执行上下文的栈结构； 

 执行上下文：Execution Context，代码在执行之前会先创建对应的执行上下文； 

 变量对象：Variable Object，上下文关联的VO对象，用于记录函数和变量声明； 

 全局对象：Global Object，全局执行上下文关联的VO对象； 

 激活对象：Activation Object，函数执行上下文关联的VO对象； 

 作用域链：scope chain，作用域链，用于关联指向上下文的变量查找； 

◼ **在新的ECMA代码执行描述中（ES5以及之上），对于代码的执行流程描述改成了另外的一些词汇：** 

 基本思路是相同的，只是对于一些词汇的描述发生了改变； 

 执行上下文栈和执行上下文也是相同的；

## 词法环境

◼ **词法环境是一种规范类型，用于在词法嵌套结构中定义关联的变量、函数等标识符；** 

 一个词法环境是由环境记录（Environment Record）和一个外部词法环境（o*ute;r* Lexical Environment）组成； 

 一个词法环境经常用于关联一个函数声明、代码块语句、try-catch语句，当它们的代码被执行时，词法环境被创建出来； 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595390273-18ab469e-3415-458c-b936-2b71ca23d223.png)

◼ **也就是在ES5之后，执行一个代码，通常会关联对应的词法环境；** 

 那么执行上下文会关联哪些词法环境呢？

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595395099-333f3bbd-8c59-4c8b-9ffc-1c3479df132b.png)

## LexicalEnvironment和VariableEnvironment

◼ LexicalEnvironment用于处理let、const声明的标识符： 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595525959-946f917e-f770-4f67-8ebf-ff6b151183b1.png)

◼ VariableEnvironment用于处理var和function声明的标识符：

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595534632-659943c6-0f71-4835-a1a0-306bc21442e7.png)

## 环境记录

◼ **在这个规范中有两种主要的环境记录值:声明式环境记录和对象环境记录。** 

 声明式环境记录：声明性环境记录用于定义ECMAScript语言语法元素的效果，如函数声明、变量声明和直接将标识符绑定与ECMAScript语言值关联起来的Catch子句。 

 对象式环境记录：对象环境记录用于定义ECMAScript元素的效果，例如WithStatement，它将标识符绑定与某些对象的属性关联起来。

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595565536-448052e6-b83b-4e0b-a63b-15d26941bdea.png)

## 新的ECMA描述内存图

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595580672-319ae8e1-b4da-46b1-af14-2598b8f8cde0.png)

# let、const的使用

◼ **在ES5中我们声明变量都是使用的var关键字，从ES6开始新增了两个关键字可以声明变量：let、const** 

 let、const在其他编程语言中都是有的，所以也并不是新鲜的关键字； 

 但是let、const确确实实给JavaScript带来一些不一样的东西； 

◼ **let关键字：** 

 从直观的角度来说，let和var是没有太大的区别的，都是用于声明一个变量； 

◼ **const关键字：** 

 const关键字是constant的单词的缩写，表示常量、衡量的意思； 

 它表示保存的数据一旦被赋值，就不能被修改； 

 但是如果赋值的是引用类型，那么可以通过引用找到对应的对象，修改对象的内容； 

◼ 注意： 

 另外let、const不允许重复声明变量；

## let/const作用域提升

◼ **let、const和var的另一个重要区别是作用域提升：** 

 我们知道var声明的变量是会进行作用域提升的； 

 但是如果我们使用let声明的变量，在声明之前访问会报错； 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595626876-a51462cf-fd03-4259-9d80-ef4667760a7d.png)

◼ **那么是不是意味着foo变量只有在代码执行阶段才会创建的呢？** 

 事实上并不是这样的，我们可以看一下ECMA262对let和const的描述； 

 **这些变量会被创建在包含他们的词法环境被实例化时，但是是不可以访问它们的，直到词法绑定被求值；**

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595642451-f6f6e306-7800-42ab-9e5e-9885afc39413.png)

## 暂时性死区

◼ **我们知道，在let、const定义的标识符真正执行到声明的代码之前，是不能被访问的** 

 从块作用域的顶部一直到变量声明完成之前，这个变量处在暂时性死区（TDZ，temporal dead zone） 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595699834-e34341a3-f7cf-41a6-bc23-04733ac19be9.png)

◼ 使用术语 “temporal” 是因为区域取决于执行顺序（时间），而不是编写代码的位置；

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595703152-27548ce2-166b-4986-8ee9-4c48951d0de5.png)

## let/const有没有作用域提升呢？

◼ **从上面我们可以看出，在****执行上下文的词法环境创建出来的时候****，****变量事实上已经被创建****了，只是****这个变量是不能被访问****的。** 

 那么变量已经有了，但是不能被访问，是不是一种作用域的提升呢？ 

◼ **事实上维基百科并没有对作用域提升有严格的概念解释，那么我们自己从字面量上理解；** 

 **作用域提升：**在声明变量的作用域中，如果这个变量可以在声明之前被访问，那么我们可以称之为作用域提升； 

 在这里，它虽然被创建出来了，但是不能被访问，我认为不能称之为作用域提升； 

◼ 所以我的观点是let、const没有进行作用域提升，但是会在解析阶段被创建出来。

## Window对象添加属性

◼ **我们知道，在全局通过var来声明一个变量，事实上会在window上添加一个属性：** 

 但是let、const是不会给window上添加任何属性的。 

◼ **那么我们可能会想这个变量是保存在哪里呢？**

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595821381-70a75db3-5cfa-4551-b27a-be977c7de9fd.png)

# 块级作用域的使用

## var的块级作用域

◼ 在我们前面的学习中，JavaScript只会形成两个作用域：全局作用域和函数作用域。 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595858846-74d1d883-afad-4c74-b4f5-686809def2ee.png)

◼ ES5中放到一个代码中定义的变量，外面是可以访问的：

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595866765-dc22c25b-9bbe-4f3d-9032-b3812e00c1e5.png)

## let/const的块级作用域

◼ **在ES6中新增了块级作用域，并且通过****let、const、function、class声明****的标识符是具备块级作用域的限制的：** 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595900905-2ff98e06-1542-4e19-8e23-29e3db0a9afc.png)

◼ **但是我们会发现****函数拥有块级作用域****，但是****外面依然是可以访问****的：** 

 这是因为引擎会对函数的声明进行特殊的处理，允许像var那样进行提升； 

## 块级作用域的应用

◼ **我来看一个实际的案例：获取多个按钮监听点击** 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595942965-bf2ecf3d-65f5-4d02-99b8-ae2829200e15.png)

◼ **使用let或者const来实现：**

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595947041-79bf19b6-f7a3-4143-aa1b-8b6260867f4c.png)

## var、let、const的选择

◼ **那么在开发中，我们到底应该选择使用哪一种方式来定义我们的变量呢？** 

◼ **对于var的使用：** 

 我们需要明白一个事实，var所表现出来的特殊性：比如作用域提升、window全局对象、没有块级作用域等都是一些历史遗 

留问题； 

 其实是JavaScript在设计之初的一种语言缺陷； 

 当然目前市场上也在利用这种缺陷出一系列的面试题，来考察大家对JavaScript语言本身以及底层的理解； 

 但是在实际工作中，我们可以使用最新的规范来编写，也就是不再使用var来定义变量了； 

◼ **对于let、const：** 

 对于let和const来说，是目前开发中推荐使用的； 

 我们会优先推荐使用const，这样可以保证数据的安全性不会被随意的篡改； 

 只有当我们明确知道一个变量后续会需要被重新赋值时，这个时候再使用let； 

 这种在很多其他语言里面也都是一种约定俗成的规范，尽量我们也遵守这种规范；

# 模板字符串的详解

## 字符串模板基本使用

◼ **在ES6之前，如果我们想要将字符串和一些动态的变量（标识符）拼接到一起，是非常麻烦和丑陋的（ugly）**。 

◼ **ES6允许我们使用字符串模板来嵌入JS的变量或者表达式来进行拼接：** 

 首先，我们会使用 **``** 符号来编写字符串，称之为模板字符串； 

 其次，在模板字符串中，我们可以通过 **${expression}** 来嵌入动态的内容；

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596026402-fd136b60-218e-4a5a-8c7b-4ce728957e2e.png)

## 标签模板字符串使用

◼ **模板字符串还有另外一种用法：标签模板字符串（Tagged Template Literals）。** 

◼ **我们一起来看一个普通的JavaScript的函数：** 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596047697-74f202ec-cfef-4a5e-ac49-6ee097e075bf.png)

◼ **如果我们使用标签模板字符串，并且在调用的时候插入其他的变量：** 

 模板字符串被拆分了； 

 第一个元素是数组，是被模块字符串拆分的字符串组合； 

 后面的元素是一个个模块字符串传入的内容；

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596054621-9e9d41a4-87a1-44f6-9aec-c76321d66e52.png)

# ES6函数的增强用法

## React的styled-components库

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596128181-d45956a5-a631-4153-ae77-b5ee8871d996.png)

## 函数的默认参数

◼ **在ES6之前，我们编写的函数参数是没有默认值的，所以我们在编写函数时，如果有下面的需求：** 

 传入了参数，那么使用传入的参数； 

 没有传入参数，那么使用一个默认值； 

◼ **而在ES6中，我们允许给函数一个默认值：** 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596152539-617dd04b-3d4c-4b6b-91f5-27aa6c676012.png)

## 函数默认值的补充

◼ **默认值也可以和解构一起来使用：** 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596193970-a1f49f61-8513-47cf-88f2-fce3e9499669.png)

◼ **另外参数的默认值我们通常会将其放到最后（在很多语言中，如果不放到最后其实会报错的）：** 

 但是JavaScript允许不将其放到最后，但是意味着还是会按照顺序来匹配； 

◼ **另外默认值会改变函数的length的个数，默认值以及后面的参数都不计算在length之内了。**

## 函数的剩余参数（已经学习）

◼ **ES6中引用了rest parameter，可以将不定数量的参数放入到一个数组中：** 

 如果最后一个参数是 ... 为前缀的，那么它会将剩余的参数放到该参数中，并且作为一个数组； 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596225843-a7b83545-dbd1-413b-b612-1912253a57be.png)

◼ **那么剩余参数和arguments有什么区别呢？** 

 剩余参数只包含那些没有对应形参的实参，而 arguments 对象包含了传给函数的所有实参； 

 arguments对象不是一个真正的数组，而rest参数是一个真正的数组，可以进行数组的所有操作； 

 arguments是早期的ECMAScript中为了方便去获取所有的参数提供的一个数据结构，而rest参数是ES6中提供并且希望以此 

来替代arguments的； 

◼ **注意：剩余参数必须放到最后一个位置，否则会报错。**

## 函数箭头函数的补充

◼ **在前面我们已经学习了箭头函数的用法，这里进行一些补充：** 

 箭头函数是没有显式原型prototype的，所以不能作为构造函数，使用new来创建对象； 

 箭头函数也不绑定this、arguments、super参数；

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596262947-b632e32a-473d-4a16-a1e0-7e83e336e2ee.png)

# 展开运算符的使用

## 展开语法

◼ **展开语法(Spread syntax)**： 

 可以在函数调用/数组构造时，将数组表达式或者string在语法层面展开； 

 还可以在构造字面量对象时, 将对象表达式按key-value的方式展开； 

◼ **展开语法的场景：** 

 在函数调用时使用； 

 在数组构造时使用； 

 在构建对象字面量时，也可以使用展开运算符，这个是在ES2018（ES9）中添加的新特性； 

◼ **注意：展开运算符其实是一种浅拷贝；**

## 数值的表示

◼ 在ES6中规范了二进制和八进制的写法： 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596311898-283d3402-92c1-4e85-837e-dc80b25d3d67.png)	

◼ 另外在ES2021新增特性：数字过长时，可以使用_作为连接符

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596316010-2d75231b-f5b6-46d9-940f-f7edccc1c50a.png)

# Symbol类型用法

## Symbol的基本使用

◼ Symbol是什么呢？Symbol是ES6中新增的一个基本数据类型，翻译为符号。 

◼ **那么为什么需要Symbol呢？** 

 在ES6之前，对象的属性名都是字符串形式，那么很容易造成属性名的冲突； 

 比如原来有一个对象，我们希望在其中添加一个新的属性和值，但是我们在不确定它原来内部有什么内容的情况下，很容易 

造成冲突，从而覆盖掉它内部的某个属性； 

 比如我们前面在讲apply、call、bind实现时，我们有给其中添加一个fn属性，那么如果它内部原来已经有了fn属性了呢？ 

 比如开发中我们使用混入，那么混入中出现了同名的属性，必然有一个会被覆盖掉； 

◼ Symbol就是为了解决上面的问题，用来**生成一个独一无二的值**。 

 Symbol值是通过Symbol函数来生成的，生成后可以作为属性名； 

 也就是在ES6中，对象的属性名可以使用字符串，也可以使用Symbol值； 

◼ **Symbol即使多次创建值，它们也是不同的：**Symbol函数执行后每次创建出来的值都是独一无二的； 

◼ **我们也可以在创建Symbol值的时候传入一个描述description**：这个是ES2019（ES10）新增的特性；

## Symbol作为属性名

◼ 我们通常会使用Symbol在对象中表示唯一的属性名：

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596365051-8a226bb2-efe9-462b-bf37-d67170fc5a06.png)

## 相同值的Symbol

◼ **前面我们讲Symbol的目的是为了创建一个独一无二的值，那么如果我们现在就是想创建相同的Symbol应该怎么来做呢？** 

 我们可以使用Symbol.for方法来做到这一点； 

 并且我们可以通过Symbol.keyFor方法来获取对应的key；

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596388669-f60fefaf-620f-42bb-bc36-8526eb33042c.png)

# 数据结构-Set集合

## Set的基本使用

◼ **在ES6之前，我们存储数据的结构主要有两种：****数组、对象****。** 

 **在ES6中新增了另外两种数据结构：****Set、Map****，以及它们的另外形式WeakSet、WeakMap**。 

◼ **Set是一个新增的数据结构，可以用来保存数据，类似于数组，但是和数组的区别是****元素不能重复****。** 

 创建Set我们需要通过Set构造函数（暂时没有字面量创建的方式）： 

◼ 我们可以发现Set中存放的元素是不会重复的，那么Set有一个非常常用的功能就是给数组去重。

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596426068-731f4402-74be-49c9-b147-c9b748d1ac88.png)

## Set的常见方法

◼ **Set常见的属性：** 

 size：返回Set中元素的个数； 

◼ **Set常用的方法：** 

 add(value)：添加某个元素，返回Set对象本身； 

 delete(value)：从set中删除和这个值相等的元素，返回boolean类型； 

 has(value)：判断set中是否存在某个元素，返回boolean类型； 

 clear()：清空set中所有的元素，没有返回值； 

 forEach(callback, [, thisArg])：通过forEach遍历set； 

◼ **另外Set是支持for of的遍历的。**

## WeakSet的使用

◼ **和Set类似的另外一个数据结构称之为****WeakSet****，也是内部元素不能重复的数据结构。** 

◼ **那么和Set有什么区别呢？** 

 区别一：WeakSet中只能存放对象类型，不能存放基本数据类型； 

 区别二：WeakSet对元素的引用是弱引用，如果没有其他引用对某个对象进行引用，那么GC可以对该对象进行回收； 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596533248-d03e0f77-d058-48ae-b9b5-d9b69e0ae37d.png)

◼ **WeakSet常见的方法：** 

 add(value)：添加某个元素，返回WeakSet对象本身； 

 delete(value)：从WeakSet中删除和这个值相等的元素，返回boolean类型； 

 has(value)：判断WeakSet中是否存在某个元素，返回boolean类型；

## WeakSet的应用

◼ **注意：WeakSet不能遍历** 

 因为WeakSet只是对对象的弱引用，如果我们遍历获取到其中的元素，那么有可能造成对象不能正常的销毁。 

 所以存储到WeakSet中的对象是没办法获取的； 

◼ **那么这个东西有什么用呢？** 

 事实上这个问题并不好回答，我们来使用一个Stack Overflow上的答案；

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596564573-fd8b6334-4abb-4f33-80f2-999de9074e7e.png)

# 数据结构 - Map映射

## Map的基本使用

◼ **另外一个新增的数据结构是Map，用于****存储映射关系****。** 

◼ **但是我们可能会想，在之前我们可以****使用对象来存储映射关系，他们有什么区别****呢？** 

 事实上我们对象存储映射关系只能用字符串（ES6新增了Symbol）作为属性名（key）； 

 某些情况下我们可能希望通过其他类型作为key，比如对象，这个时候会自动将对象转成字符串来作为key； 

◼ **那么我们就可以使用Map：**

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596594339-eaa199f7-330c-43c3-b8ca-968f5c0345eb.png)

## Map的常用方法

◼ **Map常见的属性：** 

 size：返回Map中元素的个数； 

◼ **Map常见的方法：** 

 set(key, value)：在Map中添加key、value，并且返回整个Map对象； 

 get(key)：根据key获取Map中的value； 

 has(key)：判断是否包括某一个key，返回Boolean类型； 

 delete(key)：根据key删除一个键值对，返回Boolean类型； 

 clear()：清空所有的元素； 

 forEach(callback, [, thisArg])：通过forEach遍历Map； 

◼ **Map也可以通过for of进行遍历。**

## WeakMap的使用

◼ **和Map类型的另外一个数据结构称之为****WeakMap****，也是****以键值对的形式****存在的。** 

◼ 那么和Map有什么区别呢？ 

 区别一：WeakMap的key只能使用对象，不接受其他的类型作为key； 

 区别二：WeakMap的key对对象想的引用是弱引用，如果没有其他引用引用这个对象，那么GC可以回收该对象； 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596650541-50a4ab12-e05f-4fc8-982a-1827f0b9a079.png)

◼ **WeakMap常见的方法有四个：** 

 set(key, value)：在Map中添加key、value，并且返回整个Map对象； 

 get(key)：根据key获取Map中的value； 

 has(key)：判断是否包括某一个key，返回Boolean类型； 

 delete(key)：根据key删除一个键值对，返回Boolean类型； 

## WeakMap的应用

◼ **注意：WeakMap也是不能遍历的** 

 没有forEach方法，也不支持通过for of的方式进行遍历； 

◼ **那么我们的WeakMap有什么作用呢？（后续专门讲解）**

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673596673930-9d45435a-2310-496b-adb0-a35f1e2d62e4.png)

# ES6其他知识点说明

◼ **事实上ES6（ES2015）是一次非常大的版本更新，所以里面重要的特性非常多：** 

 除了前面讲到的特性外还有很多其他特性； 

◼ **Proxy、Reflect，我们会在后续专门进行学习。** 

 并且会利用Proxy、Reflect来讲解Vue3的响应式原理； 

◼ **Promise，用于处理异步的解决方案** 

 后续会详细学习； 

 并且会学习如何手写Promise； 

◼ **ES Module模块化开发：** 

 从ES6开发，JavaScript可以进行原生的模块化开发； 

 这部分内容会在工程化部分学习； 

 包括其他模块化方案：CommonJS、AMD、CMD等方案；

# ES7新增特征

## ES7 - Array Includes

◼ 在ES7之前，如果我们想判断一个数组中是否包含某个元素，需要通过 indexOf 获取结果，并且判断是否为 -1。 

◼ 在ES7中，我们可以通过**includes**来判断一个数组中是否包含一个指定的元素，根据情况，如果包含则返回 true，否则返回false。

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673594594433-80d373a6-5fbe-4a24-8c3f-0fc8febe6173.png)

## ES7 - 指数exponentiation运算符

◼ 在ES7之前，计算数字的乘方需要通过 Math.pow 方法来完成。 

◼ 在ES7中，增加了 ***\* 运算符**，可以对数字来计算乘方。

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673594631796-d7e0eb72-907a-49f9-8029-97b960139435.png)

# ES8新增特征

## ES8 - Object values

◼ 之前我们可以通过 Object.keys 获取一个对象所有的key 

◼ **在ES8中提供了** **Object.values** **来获取所有的value值：**

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673594661878-a59e8396-1dcf-446d-8215-3ad83a5ef4ec.png)

## ES8 - Object entries

◼ **通过** **Object.entries** **可以获取到一个数组，数组中会存放可枚举属性的键值对数组。** 

 可以针对对象、数组、字符串进行操作；

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673594700805-dd9ad81b-b51b-44a3-a7c0-7f4a8c727136.png)

## ES8 - String Padding

◼ 某些字符串我们需要对其进行前后的填充，来实现某种格式化效果，ES8中增加了 padStart 和 padEnd 方法，分别是对字符串 

的首尾进行填充的。 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673594734344-a99045cb-e250-4c3f-9b2d-70bd65bbedd1.png)

◼ **我们简单具一个应用场景：比如需要对身份证、银行卡的前面位数进行隐藏：**

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673594740863-ab594c46-13cc-4d66-bfd2-edd961f28059.png)

## ES8 - Trailing Commas

◼ **在ES8中，我们允许在函数定义和调用时****多加一个逗号****：**

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673594763181-94a30d14-a531-488c-918a-7654a644d88c.png)

## ES8 - Object Descriptors

◼ **Object.getOwnPropertyDescriptors ：** 

 这个在之前已经讲过了，这里不再重复。 

◼ **Async Function**：**async、await** 

 后续讲完Promise讲解

# ES9新增特征

◼ **Async iterators：后续迭代器讲解** 

◼ **Object spread operators：前面讲过了** 

◼ **Promise finally：后续讲Promise讲解**

# ES10新增特征

## ES10 - flat flatMap

◼ flat() 方法会按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组中的元素合并为一个新数组返回。 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673594831366-88abd6d0-2584-41eb-adde-9bbe7e44c4cc.png)

◼ flatMap() 方法首先使用映射函数映射每个元素，然后将结果压缩成一个新数组。 

 注意一：flatMap是先进行map操作，再做flat的操作； 

 注意二：flatMap中的flat相当于深度为1；

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673594838765-7f63e826-37e8-46d1-baef-2fbc12255ec7.png)

## ES10 - Object fromEntries

◼ **在前面，我们可以通过 Object.entries 将一个对象转换成 entries** 

◼ **那么如果我们有一个entries了，如何将其转换成对象呢？** 

 ES10提供了 Object.formEntries来完成转换： 

◼ **那么这个方法有什么应用场景呢？**

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673594863188-cbc129dd-e263-4a7a-8e3f-ce1360818f18.png)

## ES10 - trimStart trimEnd

◼ **去除一个字符串首尾的空格，我们可以通过trim方法，如果单独去除前面或者后面呢？** 

 ES10中给我们提供了trimStart和trimEnd

## ES10 其他知识点

◼ **Symbol description：已经讲过了** 

◼ **Optional catch binding：后面讲解try cach讲解**

# ES11新增特征

## ES11 - BigInt

◼ **在早期的JavaScript中，我们不能正确的表示过大的数字：** 

 大于MAX_SAFE_INTEGER的数值，表示的可能是不正确的。 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673594938516-0ac2046e-274e-41ea-8194-fa4876595769.png)

◼ **那么ES11中，引入了新的数据类型BigInt，用于表示大的整数：** 

 BitInt的表示方法是在数值的后面加上n

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673594944024-cd87dc3b-dc17-42d0-8d60-1ceba02819fb.png)

## ES11 - Nullish Coalescing Operator

◼ **ES11，Nullish Coalescing Operator增加了空值合并操作符：**

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673594962710-02a2d73e-9492-4f62-a778-2cb03a88f256.png)

## ES11 - Optional Chaining

◼ **可选链****也是****ES11中新增一个特性****，主要作用是让我们的代码在****进行null和undefined判断时更加清晰****和简洁：**

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673594984963-8e6b2d05-2f6f-4606-b451-92709d7b3051.png)

## ES11 - Global This（已学）

◼ **在之前我们希望获取JavaScript环境的全局对象，不同的环境获取的方式是不一样的** 

 比如在浏览器中可以通过this、window来获取； 

 比如在Node中我们需要通过global来获取； 

◼ **在ES11中对获取全局对象进行了统一的规范：globalThis**

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595005600-597b4fa6-8fc8-4666-b3e1-a7c78eba0cbf.png)

## ES11 - for..in标准化

◼ **在ES11之前，虽然很多浏览器支持for...in来遍历****对象类型****，但是并没有被ECMA标准化。** 

◼ **在ES11中，对其进行了标准化，****for...in是用于遍历对象****的key的：**

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595029141-9326b0cf-dccc-410c-b23f-ee5ec38d0f54.png)

## ES11其他知识点

◼ **Dynamic Import：**后续ES Module模块化中讲解。 

◼ **Promise.allSettled：**后续讲Promise的时候讲解。 

◼ **import meta：**后续ES Module模块化中讲解。

# ES12新增特征

## ES12 - FinalizationRegistry

◼ **FinalizationRegistry** **对象可以让你在对象被垃圾回收时请求一个回调。** 

 FinalizationRegistry 提供了这样的一种方法：当一个在注册表中注册的对象被回收时，请求在某个时间点上调用一个清理回 

调。（清理回调有时被称为 finalizer ）; 

 你可以通过调用register方法，注册任何你想要清理回调的对象，传入该对象和所含的值;

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595069977-d508112f-86ac-4a94-ab8e-75beff46f830.png)

## ES12 - WeakRefs

◼ 如果我们默认将一个对象赋值给另外一个引用，那么这个引用是一个强引用： 

 如果我们希望是一个弱引用的话，可以使用WeakRef；

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595087649-48a32e08-6756-44c4-af8f-7e9a2026211d.png)

## ES12 - logical assignment operators

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595101738-95a2f5f3-a1f0-4d8a-9b78-91eaae0fa537.png)

## ES12其他知识点

◼ **Numeric Separator：讲过了；** 

◼ **String.replaceAll：字符串替换；**

# ES13新增特征

## ES13 - method .at()

◼ 前面我们有学过字符串、数组的at方法，它们是作为ES13中的新特性加入的：

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595143729-d52992d4-8489-43bd-b865-c195dc345fa9.png)

## ES13 - Object.hasOwn(obj, propKey)

◼ Object中新增了一个静态方法（类方法）： hasOwn(obj, propKey) 

 该方法用于判断一个对象中是否有某个自己的属性； 

◼ 那么和之前学习的Object.prototype.hasOwnProperty有什么区别呢？ 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595171020-1f4d7f69-c0ad-4e22-9717-d8d2f3ded6a3.png)

 区别一：防止对象内部有重写hasOwnProperty 

 区别二：对于隐式原型指向null的对象， hasOwnProperty无法进行判断

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595179341-92acfeb1-31d2-4ae3-9e1e-1314a9638d1e.png)

## ES13 - New members of classes

◼ 在ES13中，新增了定义class类中成员字段（field）的其他方式： 

 Instance public fields 

 Static public fields 

 Instance private fields 

 static private fields 

 static block 

![img](https://cdn.nlark.com/yuque/0/2023/png/34886243/1673595200512-5681371c-d38c-424e-8306-95a8af41ac1b.png)