  ## Axios特征
  1. promise化
  2. 同构化  同时支持浏览器和node环境
  3. 直接拦截，转换 请求和响应
  4. 支持取消请求
  
  ## 请求配置
  ```js
  {
    url: '/user', // 必须
    method: 'get', // 默认是get
    baseURL: 'https://some-domain.com/api/',
    transformRequest: [function(data, headers) {
      // 对发送的请求做任意转换， 这个用的很少
      return data;
    }],
    transformResponse: [function (data) {
    // 对接收的 data 进行任意转换处理

    return data;
  }],
  headers: { 'X-Requested-with': 'XMLHttpRequest'}, // 自定义请求
  // params 是请求url参数  必须是一个简单对象或者URlSearchParams 这里注意  url 意味着这个主要是get方法使用  这和后面后面的data有很大区别
  params: {
    ID: 123,
  },
  // `data` 是作为请求体被发送的数据
  // 仅适用 'PUT', 'POST', 'DELETE 和 'PATCH' 请求方法
  // 在没有设置 `transformRequest` 时，则必须是以下类型之一:
  // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
  // - 浏览器专属: FormData, File, Blob
  // - Node 专属: Stream, Buffer
  data: {
    name: 'nice',
  },
  timeout: 1000 , // 请求超时
  // `withCredentials` 表示跨域请求时是否需要使用凭证
  withCredentials: false, // default
  // `adapter` 允许自定义处理请求，这使测试更加容易。
  // 返回一个 promise 并提供一个有效的响应 （参见 lib/adapters/README.md）。
  adapter: function (config) {
    /* ... */
  },
  // `auth` HTTP Basic Auth
  auth: {
    username: 'janedoe',
    password: 's00pers3cret'
  },
   // `responseType` 表示浏览器将要响应的数据类型
  // 选项包括: 'arraybuffer', 'document', 'json', 'text', 'stream'
  // 浏览器专属：'blob'
  responseType: 'json', // 默认值




  }
  ```