## DOM及其基础操作

document object model 文档对象模型，提供一些属性和方法在我们操作页面中的元素

#### 获取DOM元素的方法

- document.getElementById()	指定在文档中，基于元素的ID获取这个元素对象
- [context].getElementByTagName()   在指定上下文（容器）中，通过标签名获取一组元素集合
- [context].getElementByClassName()  在指定上下文中，通过样式类名获取一组元素集合（不兼容IE678）
- document.getElementByName() 在整个文档中，基于元素的name属性获取一组元素属性集合（在IE中只有表单元素的NAME才能识别，所以我们一般应用于表单元素处理）
- document.head/body/documentElement 获取页面中的head、body、html三个元素
- [context].querySelector([selector]) 在指定上下文中，通过选择器获取到指定的元素对象（不兼容IE678）
- [context].querySelectorAll([selector])在指定上下文中，通过选择器获取到指定的元素对象集合（不兼容IE678）

#### JS中的节点和描述节点之间的关系的属性

节点：Node（页面中所有的东西都是节点）

节点集合：NodeList（getElementsByName/querySelectorAll获取到的都是节点集合）

- 元素节点
  - nodetype：1
  - nodename：大写的标签名
  - nodevalue：null
- 文本节点
  - nodetype：3
  - nodename：'#text'
  - nodevalue：注释内容
- 注释节点
  - nodetype：8
  - nodename：’#commen‘
  - nodevalue：注释内容
- 文档节点
  - nodetype：9
  - nodename：'#document'
  - nodevalue：null

#### 描述这些节点之间关系的属性

- childnodes：获取所有的子节点
  - 标准浏览器（非IE678）中会把空格和换行当做文本节点处理（childNodes包含所有节点）
  - 只想要元素节点（但是IE678下使用children会把注释也当做节点）
- children：获取所有的元素子节点（元素标签集合）
- firstchild：获取第一个子节点
- lastchild：获取最后一个子节点
- firstElementChild/lastElementChild：获取第一个和最后一个元素子节点（不兼容IE678）
- previousSibling：获取上一个哥哥节点.
- nextSibling：获取下一个弟弟节点
- parent：获取父节点
- previousElementSibling ：获取上一个元素哥哥节点
- nextElementSibling：获取下一个元素弟弟节点

```

// children ：获取指定上下文中所有元素自己点
// @params
//     context [element object] 指定上下文元素信息
// @return
//         [array]  返回所有元素子节点

function children(context) {
    var resAry = [];
    // 1.获取到所有元素的子节点
    var allNodechild = context.hasChildNodes;

    for(var i = 0; i<allNodechild.length;i++){
        var item = allNodechild(i);
        item.nodeType === 1 ? resAry.push(item) : null;
    }
    return resAry;
}
console.log(children(box));
```

#### 在JS中动态增删改元素

- createElement 创建元素对象

  - ```
    var box = document.createElement('div')
    ```

- creatNodeElement 创建文本对象

  - ```
    var span = document.querySelector(span);
    ```

- appendchild 把节点添加到容器末位

  - ```
    document.body.appendChild(box)
    ```

- insertBefore 把节点添加到制定容器中的指定元素的前面

  - ```
    父节点.InsertBefore(需要插入到节点,beforeElement)
    // document.body.insertBefore(box,span);
    ```

- cloneNode（true/false）克隆元素或者节点

  - ```
    cloneNode()的参数为false时，浅克隆，为true时，深克隆
    var liclone = li.cloneNode(false);
        console.log(liclone);
        // var liclone = li.cloneNode(true);
        // console.log(liclone);
    ```

- removeChild 移除容器中某个元素

  

自定义属性的另一种添加方式

setAttribute/getAttribute/removeAttribute		设置于获取移出元素的自定义属性信息（这种方式是把自定义属性放到元素结构上）

```
<button>1</button>
<button>2</button>
<button>3</button>
<script>
  var btns = document.querySelectorAll("button");
  for(var i = 0;i<btns.length;i++){
    // 实现原理1：通过给对象（堆内存）添加一个新的属性，来讲每一个I的值，进行保存，在使用的时候去对象身上寻找这个属性
    // btns[i].myIndex = i;

      // 实现原理2：给相对应的标签添加自有属性并保存相应的值，在需要的时候，通过标签的属性去获取这个值

    // 注意：通过给对象添加属性的方式，只能用对象的获取方式(obj.属性名),设置在元素结构上的内容只能通过相对应的方式来获取（getAttribute）
    var btn = btns[i];
    btn.setAttribute('myIndex',i);
    btn.onclick = function (){
      alert(this.getAttribute('myIndex'));
    }
  }
  var btn = document.querySelector('button');
    btn.removeAttribute('myIndex');
</script>
```

