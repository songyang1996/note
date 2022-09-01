
# script标签的async和defer属性

- 标记 defer 时

异步获取脚本， 不会停止 HTML 渲染， 在 DOM 事件 domInteractive 之后， 开始执行脚本， 执行完成之后， 触发 domComplete 事件， 然后是 onLoad 事件。

- 标记 async 时

异步获取脚本， 之后如果 HTML 没有渲染完毕， 中断 HTML 渲染， 执行脚本， 然后继续渲染后续的 HTML 内容。

## 相同点

- 加载文件时不阻塞页面渲染
- 对于 inline 的 script 无效（只适用有src的外部 js）
- 使用这两个属性的脚本中不能调用 document.write 方法
- 有脚本的 onload 的事件回调

## 区别点

- html4.0 中定义了 defer；html5.0 中定义了 async
- 浏览器支持不同
- 每一个 async 属性的脚本都在它下载结束之后立刻执行，同时会在 window 的 load 事件之前执行。所以就有可能出现脚本执行顺序被打乱的情况；每一个 defer 属性的脚本都是在页面解析完毕之后，按照原本的顺序执行，同时会在 document 的 DOMContentLoaded 之前执行

## 一般的用法

通常来说，尽可能使用async，然后是defer，最后不使用属性。 并遵循以下规则：

如果脚本是模块化的，并且不依赖于任何脚本，则使用async。
如果脚本依赖于或依赖于另一个脚本，则使用defer。
如果脚本很小并且有async脚本依赖该脚本，则不加属性。
