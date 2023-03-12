---
title: React路由实现
date: 2023-03-11 22:30:15
updated: 2023-03-12 10:07:18
cover: https://pi.loili.com/2023/1c4f5102a78ba7fec349dc73a5e2c1a3.png
categories:
  - web
  - 前端
tags:
  - React
  - 前端
  - web
  - React Router
---

## 核心组件 - BrowserRouter

**作用**：包裹整个应用，一个 React 应用只需要使用一次

**两种常用 Router**：HashRouter 和 BrowserRouter (推荐)

```jsx
function App() {
  return (
    <BrowserRouter>
      <Link to="/">首页</Link>
      <Link to="/about">关于</Link>
      <Routes>
        <Route path="/" element={ <Home /> }></Route>
        <Route path="/about" element={ <About />}></Route>
    </BrowserRouter>
  )
}
```

## 核心组件 - Link

**作用**：用于指定导航链接，完成路由转跳

**语法说明**：组件通过 `to` 属性指定路由地址，最终会渲染为 `a` 链接元素

```jsx
<Link to="/path">页面一</Link>
```

## 核心组件 - Routes

**作用**：提供一个路由出口，满足条件的路由组件会渲染到组件内部

```jsx
<Routes>
  {/* 满足条件的路由组件会渲染到这里 */}
  <Route />
  <Route />
</Routes>
```

## 核心组件 - Route

**作用**：用于指定导航链接，完成路由匹配

```jsx
<Route path="/about" element={ <About/> }/>
```

说明：当路径为 `/about` 时，会渲染 `About` 组件

## 编程式导航

### 跳转

**作用**：通过 JS 编程的方式进行路由页面转跳，比如从登录页转到关于页

**语法说明**：

1. 导入 `useNavigate` 钩子函数
2. 执行钩子函数得到转跳函数
3. 执行转跳函数完成转跳

```jsx
import { useNavigate } from 'react-router-dom'

const Login = () => {
  const navigage = useNavigate()
  const goAbout = () => {
    navigage('/about',{ replace: true }) // 如果为 true，会以替换的方式进行跳转（无法返回上一页），而不是叠加。
  }
  return (
    <div>
      Login
      <button onClick={ goAbout }>转跳关于</button>
    </div>
  )
}

export default Login
```

### 转跳携带跳转参数

**场景**：有些时候不光需要跳转路由还需要传递参数

**两种方式**：

1. `searchParams` 传参
   传参：
   ```jsx
   navigage('/about?id=1001')
   ```
   取参
   ```jsx
   let [params] = useSearchParams()
   let id = params.get('id')
   ```

2. `params` 传参
   传参：
   ```jsx
   navigage('/about/1001')
   ```
   取参
   ```jsx
   let params = useParams()
   let id = params.id
   ```
