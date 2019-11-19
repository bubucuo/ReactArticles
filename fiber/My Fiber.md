# Fiber

[TOC]

## Fiber定义

 A Fiber is work on a Component that needs to be done or was done. There can be more than one per component.

Fiber是指组件上将要完成或者已经完成的任务，每个组件可以一个或者多个。

## Fiber字段

来自react/packages/react-reconciler/src/ReactFiber.js - Fiber



  // Tag identifying the type of fiber.

  //标记fiber的类型，类似我们之前写react核心api时候的vtype

  **tag**: WorkTag,



  // Unique identifier of this child.

  //当前子节点的唯一标识

  **key**: null | string,



  // The value of element.type which is used to preserve the identity during

  // reconciliation of this child.

  //element.type的值，保存的是协调期间当前child的身份

  **elementType**: any,



  // The resolved function/class/ associated with this fiber.

  //当前fiber关联的function或者class

  **type**: any,



  // The local state associated with this fiber.

  //当前fiber的local state

  **stateNode**: any,



  // Conceptual aliases

  // parent : Instance -> return The parent happens to be the same as the

  // return fiber since we've merged the fiber and instance.



  // Remaining fields belong to Fiber



  // The Fiber to return to after finishing processing this one.

  // This is effectively the parent, but there can be multiple parents (two)

  // so this is only the parent of the thing we're currently processing.

  // It is conceptually the same as the return address of a stack frame.

  //是指程序(program)在处理完当前fiber之后应当返回的fiber，概念上来说，这是与一个栈帧返回一个地址是相同的，它也可被认为是一个parent fiber。 

  **return**: Fiber | null,



  // Singly Linked List Tree Structure.

  //单向链表结构

  **child**: Fiber | null,

  **sibling**: Fiber | null,

  **index**: number,



  // The ref last used to attach this node.

  // I'll avoid adding an owner field for prod and model that as functions.

  **ref**: null | (((handle: mixed) => void) & {_stringRef: ?string}) | RefObject,



  // Input is the data coming into process this fiber. Arguments. Props.

  **pendingProps**: any, // This type will be more specific once we overload the tag. 在我们加载完tag之后，这个type值会更加详细

  memoizedProps: any, // The props used to create the output. 用于创建output的props值



  // A queue of state updates and callbacks.

  //用于state更新和回调的队列

  **updateQueue**: UpdateQueue<any> | null,



  // The state used to create the output

  //用于创建output的state

  **memoizedState**: any,



  // Dependencies (contexts, events) for this fiber, if it has any

  //当前fiber的依赖(上下文contexts、events事件等)，如果有的话

  **dependencies**: Dependencies | null,



  // Bitfield that describes properties about the fiber and its subtree. E.g.

  // the ConcurrentMode flag indicates whether the subtree should be async-by-

  // default. When a fiber is created, it inherits the mode of its

  // parent. Additional flags can be set at creation time, but after that the

  // value should remain unchanged throughout the fiber's lifetime, particularly

  // before its child fibers are created.

  **mode**: TypeOfMode,



  // Effect

  effectTag: SideEffectTag,



  // Singly linked list fast path to the next fiber with side-effects.

  nextEffect: Fiber | null,



  // The first and last fiber with side-effect within this subtree. This allows

  // us to reuse a slice of the linked list when we reuse the work done within

  // this fiber.

  firstEffect: Fiber | null,

  lastEffect: Fiber | null,



  // Represents a time in the future by which this work should be completed.

  // Does not include work found in its subtree.

  expirationTime: ExpirationTime,



  // This is used to quickly determine if a subtree has no pending changes.

  childExpirationTime: ExpirationTime,



  // This is a pooled version of a Fiber. Every fiber that gets updated will

  // eventually have a pair. There are cases when we can clean up pairs to save

  // memory if we need to.

  alternate: Fiber | null,



  // Time spent rendering this Fiber and its descendants for the current update.

  // This tells us how well the tree makes use of sCU for memoization.

  // It is reset to 0 each time we render and only updated when we don't bailout.

  // This field is only set when the enableProfilerTimer flag is enabled.

  actualDuration?: number,



  // If the Fiber is currently active in the "render" phase,

  // This marks the time at which the work began.

  // This field is only set when the enableProfilerTimer flag is enabled.

  actualStartTime?: number,



  // Duration of the most recent render time for this Fiber.

  // This value is not updated when we bailout for memoization purposes.

  // This field is only set when the enableProfilerTimer flag is enabled.

  selfBaseDuration?: number,



  // Sum of base times for all descendants of this Fiber.

  // This value bubbles up during the "complete" phase.

  // This field is only set when the enableProfilerTimer flag is enabled.

  treeBaseDuration?: number,



  // Conceptual aliases

  // workInProgress : Fiber ->  alternate The alternate used for reuse happens

  // to be the same as work in progress.

  // __DEV__ only

  _debugID?: number,

  _debugSource?: Source | null,

  _debugOwner?: Fiber | null,

  _debugIsCurrentlyTiming?: boolean,

  _debugNeedsRemount?: boolean,



  // Used to verify that the order of hooks does not change between renders.

  _debugHookTypes?: Array<HookType> | null,

|};



let debugCounter = 1;



function FiberNode(

  tag: WorkTag,

  pendingProps: mixed,

  key: null | string,

  mode: TypeOfMode,

) {

  // Instance

  this.tag = tag;

  this.key = key;

  this.elementType = null;

  this.type = null;

  this.stateNode = null;



  // Fiber

  this.return = null;

  this.child = null;

  this.sibling = null;

  this.index = 0;



  this.ref = null;



  this.pendingProps = pendingProps;

  this.memoizedProps = null;

  this.updateQueue = null;

  this.memoizedState = null;

  this.dependencies = null;



  this.mode = mode;



  // Effects

  this.effectTag = NoEffect;

  this.nextEffect = null;



  this.firstEffect = null;

  this.lastEffect = null;



  this.expirationTime = NoWork;

  this.childExpirationTime = NoWork;



  this.alternate = null;



  if (enableProfilerTimer) {

​    // Note: The following is done to avoid a v8 performance cliff.

​    //

​    // Initializing the fields below to smis and later updating them with

​    // double values will cause Fibers to end up having separate shapes.

​    // This behavior/bug has something to do with Object.preventExtension().

​    // Fortunately this only impacts DEV builds.

​    // Unfortunately it makes React unusably slow for some applications.

​    // To work around this, initialize the fields below with doubles.

​    //

​    // Learn more about this here:

​    // https://github.com/facebook/react/issues/14365

​    // https://bugs.chromium.org/p/v8/issues/detail?id=8538

​    this.actualDuration = Number.NaN;

​    this.actualStartTime = Number.NaN;

​    this.selfBaseDuration = Number.NaN;

​    this.treeBaseDuration = Number.NaN;



​    // It's okay to replace the initial doubles with smis after initialization.

​    // This won't trigger the performance cliff mentioned above,

​    // and it simplifies other profiler code (including DevTools).

​    this.actualDuration = 0;

​    this.actualStartTime = -1;

​    this.selfBaseDuration = 0;

​    this.treeBaseDuration = 0;

  }



  // This is normally DEV-only except www when it adds listeners.

  // TODO: remove the User Timing integration in favor of Root Events.

  if (enableUserTimingAPI) {

​    this._debugID = debugCounter++;

​    this._debugIsCurrentlyTiming = false;

  }



  if (__DEV__) {

​    this._debugSource = null;

​    this._debugOwner = null;

​    this._debugNeedsRemount = false;

​    this._debugHookTypes = null;

​    if (!hasBadMapPolyfill && typeof Object.preventExtensions === 'function') {

​      Object.preventExtensions(this);

​    }

  }

}