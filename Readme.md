# 团队作业

> 这是第一个团队作业，希望大家能以团队的方式提交答案，thx

### 现实场景

##### 我们跟后台约定一个所有请求的规范：

* 返回结构必须是：
```
{
  retcode: Number, // 可以是0(正确)，1(登陆台丢失)等等
  msg: String, // 错误时候返回的信息
  res: any // 附带的结果
}
```

* 所以我们期望能更好的错误进行处理，比如当错误产生时能直接给出错误提示

##### 并且我们希望每一种请求都可以通过 `localStorage` 做缓存

* 根据传入的 options 参数不同可以定制不同的缓存策略，例如需要有下面三种缓存策略：

```
// 0. 默认，情况下，如果没缓存，成功请求回调一次，如果有请求成功缓存应当回调两次，这样可以保证页面快速渲染，而不需要等数据返回

// 1. lazy更新，有缓存的情况下直接读取缓存，只有一次回调，但会发出请求，请求返回后只更新缓存里的数据为最新的，这样，下次再调用就能拿到这次更新的数据了

options.lazy = true

// 2. 在maxAge内使用缓存，则当发现缓存里的数据小于maxAge，则直接读取缓存，不发出任何请求，否则发出请求读取请求的数据

options.maxAge = 1000 // 即缓存是1s，也就是说这个单位是ms
```

##### 注意

* localStorage 是可能超出的所以必须对数据采取容错，并且应当有一些把低优先级的数据清除的逻辑，否则一些当前需要存储的缓存可能存储不进去

##### 实现

* 要求在 homework2 的 DB 基础上进行优化，并扩展出满足上面需求的库

* 完成所有测试用例

##### 最后希望

> 成果能使用在生产环境，所以尽量把所有边界可能都处理好