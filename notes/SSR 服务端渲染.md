# SSR 服务端渲染
优点：
* 利于SEO
* 加速首屏的渲染
* 服务端和客户端可以共享某些代码，避免重复定义

React能做到服务端渲染，主要是因为你RecatDOM

服务端渲染的API为renderToString、renderToStaticMarkup 和render的区别在于他们返回的是一段HTML字符串

前者是把React元素专成了一个HTML字符串并在服务端标识reactid
后者少了大量的reactid
* [](****)
renderToString 和 renderToStaticMarkup 可以在server端渲染你的components，其主要都是讲React Component 在Server 端转化成DOM String，也可以将props往下传，然而事件处理会失效，要到client-side的React接收到吼才会把它加上去（但要注意 server-side 和 client-side 的 checksum 要一致不然会出现错误），这样一来可以提高渲染速度和SEO效果，renderToString和renderToStaticMarkup最大的差异在于renderToStaticMarkup会少加一些React内部使用的DOM属性(eg:data-react-id)因此可以节省一些资源。





不过要注意的是如果有使用 Redux 在 Server Side Rendering 中，其流程相对复杂，不过大致流程如下： 由后端预先载入需要的 initialState，由于 Server 渲染必须全部都转成 string，所以先将 state 先 dehydration（脱水），等到 client 端再 rehydration（覆水），重建 store 往下传到前端的 React Component。

而要把资料从伺服器端传递到客户端，我们需要：

把取得初始 state 当做参数并对每个请求建立一个全新的 Redux store 实体
选择性地 dispatch 一些 action
把 state 从 store 取出来
把 state 一起传到客户端
接下来我们就开始动手实作一个简单的 React Server Side Rendering Counter 应用程式。







