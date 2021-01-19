## 2021

### 一个axiosd对请求参数编码导致的bug

```js
export const searchProfileByEmail = (query) => {
  const url    = `${ApiEndpointConstants.PROFILE_SEARCH_PATH}?email=${query}`;
  const params = {
    input_source: 'toolbox',
  };
  return api.get(url, { params });
};

// ==========================================================================

export const searchProfileByEmail = (query) => {
  const url    = `${ApiEndpointConstants.PROFILE_SEARCH_PATH}`;
  const params = {
    email                  : query,
    input_source           : 'toolbox',
  };

  return api.get(url, { params });
};
```

导致原因： axios中会自动对params部分的特殊字符做encodeURI编码处理, 但是对于URL部分不会
