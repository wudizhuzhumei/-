常见的宏任务有：
  script全文（可以看作一种宏任务）、
  setTimeout、
  setInterval、
  setImmediate（Node.js 环境）、
  I/O、
  UI渲染。

常见的微任务有：
  promise.then、
  process.nextTick（Node.js环境）、
  MutationObserver(html5新特性)，
  await表达式后面的代码。