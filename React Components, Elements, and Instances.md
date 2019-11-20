# React Components, Elements, and Instances

December 18, 2015 by [Dan Abramov](https://twitter.com/dan_abramov)

components、components的实例以及元素让很多React新手感到很迷惑。为什么有三个术语呢，明明都是一样渲染到页面上的东西？

------

**关于Instances**

如果你是位React新手，你可能只用class组件和实例。例如，你可能会通过创建一个class来声明一个Button组件。当app运行的时候，页面上的这个组件可能有几种instance，每一个都有对用的属性和state。这就是传统面向对象的UI编程。为什么我们要引入element呢？

在这种传统的UI模型中，是否关注子组件实例的创建和销毁取决于你自己。如果说一个Form组件想要渲染一个Button组件，它就需要创建这个Butto的实例，并且当有新消息的时候按时更新。

```jsx
class Form extends TraditionalObjectOrientedView {
  render() {
    // 读取需要传递给页面的数据
    const { isSubmitted, buttonText } = this.attrs;

    if (!isSubmitted && !this.button) {
      // Form还没有被提交，创建button 
      this.button = new Button({
        children: buttonText,
        color: 'blue'
      });
      this.el.appendChild(this.button.el);
    }

    if (this.button) {
      // 如果button是可见的，更新它的文本 
      this.button.attrs.children = buttonText;
      this.button.render();
    }

    if (isSubmitted && this.button) {
      // Form被提交了，销毁button
      this.el.removeChild(this.button.el);
      this.button.destroy();
    }

    if (isSubmitted && !this.message) {
      // Form被提交了，显示成功信息！
      this.message = new Message({ text: 'Success!' });
      this.el.appendChild(this.message.el);
    }
  }
}
```

这虽是伪代码，但也或多或少是你在下面这种情况下会遇到的：就像在Backbone中一样，当你以面向对象的方式写行为一致的复合UI代码的时候。
每一个组件实例必须保持它对自己DOM、子组件实例的可访问性，可以适时创建、更新、销毁。代码的行数会随着组件的state的平方数增加而增加，父组件对子组件实例有直接的访问路径，这些都使得在未来奋力开来它们而更困难。

所以React是如何与众不同的呢？

------

**element描述树**

在React中，这就是element拯救我们的地方。一个element一个对象，它能够描述一个组件实例或者是一个DOM节点和它的属性。它只包含组件类型(比如，一个Button)，它的属性(比如，它的color)，以及它包含的子元素。

一个element不是一个真正的实例，而是一种告诉React想要在屏幕上看到什么的方式。你不能在element中调用任何方法，它只是一种不变的描述对象，这个对象有两个字段：type:(string或者ReactClass)和props(objetc)。

**DOM元素**

当一个element的type值是个string的时候，它表示一个带有标签名的DOM节点，props就是它的属性。这就是React要渲染的，如下例：

```jsx
{
  type: 'button',
  props: {
    className: 'button button-blue',
    children: {
      type: 'b',
      props: {
        children: 'OK!'
      }
    }
  }
}
```

这个element只是用js对象来表示下面这样的一个HTML：

```jsx
<button class='button button-blue'>
  <b>
    OK!
  </b>
</button>
```



【2015年的，看了下，比较浅显，暂停】













