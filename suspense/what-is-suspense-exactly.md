# 用于数据获取的Suspense(实验性)

[原文地址](https://zh-hans.reactjs.org/docs/concurrent-mode-suspense.html#what-is-suspense-exactly)

> 注意：
>
> 当前页面所描述的是还未在稳定版本中可用的实验室特性，不要在app的生产版本中使用React的实验版本。这些特性在成为React一部分之前可能会在没有警告的情况下大幅度改变。
>
> 这篇文档的受众是早期的adopters和对suspense感到疑惑的人群，如果你是React新手，那你不必为这些新特性感到焦虑，因为你现在还没有必要学习它们。
>
> React16.6增加了一个<Suspense>组件，让你"等待"一些代码的加载，在等待的时候，能声明式地区分一个loading状态，比如说一个spinner。

```jsx
const ProfilePage = React.lazy(() => import('./ProfilePage')); // Lazy-loaded

// Show a spinner while the profile is loading
<Suspense fallback={<Spinner />}>
  <ProfilePage />
</Suspense>
```

数据获取的挂起是一个让你能够用<Suspense>的新特性，来声明式地等待别的东西，包括数据。当前页面聚焦于用case来获取数据，但是它也可以等待图片、scripts以及其他的异步任务。



[TOC]

------



## 到底什么是Suspense？

Suspense让组件在能渲染之前可以等待一些东西('wait' for something)，在下面的例子中，两个组件等待一个获取数据的api：

```jsx
const resource = fetchProfileData();

function ProfilePage() {
  return (
    <Suspense fallback={<h1>Loading profile...</h1>}>
      <ProfileDetails />
      <Suspense fallback={<h1>Loading posts...</h1>}>
        <ProfileTimeline />
      </Suspense>
    </Suspense>
  );
}

function ProfileDetails() {
  //尽管user info还没有加载完成，这里已经开始读取
  const user = resource.user.read();
  return <h1>{user.name}</h1>;
}

function ProfileTimeline() {
  //尽管posts还没有加载完成，这里已经开始读取
  const posts = resource.posts.read();
  return (
    <ul>
      {posts.map(post => (
        <li key={post.id}>{post.text}</li>
      ))}
    </ul>
  );
}
```



**[在 CodeSandbox试试](https://codesandbox.io/s/frosty-hermann-bztrp)**

这个例子比较简单，如果没起到作用也别担心，我们接下来继续来说它是如何工作的。记住Suspense不仅仅只是一种机制，尤其是像上面例子中用到的fetchProfileData()和resource.posts.read()这样的API并不是很重要。如果你想知道它们的定义的话，你可以看[这里](https://codesandbox.io/s/frosty-hermann-bztrp)。

Suspense不是一个数据获取库，它是数据获取库的一种机制，这种机制使得它与React对话说一个组件的数据尚未ready。React就会等待数据的ready，然后再去更新UI。在Facebook，我们用Relay和Relay的[新Suspense集成](https://relay.dev/docs/en/experimental/step-by-step)。我们希望其它像Apollo这样的库可以提供类型的集成。

长远来看，我们希望Suspense能成为组件读取异步数据的首选方式，不管这样的数据来自哪儿。



## Suspense不是什么





Suspense和现在能解决上面问题的方式全然不同，第一次读这些概念的话经常出错。我们来整理一下常见的：

它不是一个数据获取工具。它并不假设你用























