## `HttpClient` 类

如今的后端开发中，服务器之间的交互越来越多，而交互大多采用的是 Http 的对接方式，有些情况我们不想引入一个重量级的网络库，所以我封装了一个轻量的 HttpClient 类来处理这些需求。

## 如何使用

GET 请求：

~~~php
$httpClient = new HttpClient([
    'timeout' => 10,
    'headers' => [
        'User-Agent'       => 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/67.0.3396.99 Safari/537.36',
        'X-Requested-With' => 'XMLHttpRequest',
    ],
    'cookies' => [
        'PHPSESSID' => $this->sessionId,
    ],
]);
$httpClient->request('GET', 'http://www.baidu.com');
~~~

POST 请求：

~~~php
$httpClient = new HttpClient([
    'timeout' => 10,
    'headers' => [
        'access-token' => 'ACCESS_TOKEN',
    ],
]);
$headers = [
    'User-Agent'       => 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/67.0.3396.99 Safari/537.36',
];
$params = [
    'username' => '18600001111',
    'password' => '******',
];
$url = 'https://api.weixin.qq.com/cgi-bin/user/info/updateremark?access_token=ACCESS_TOKEN';
$httpClient->request('POST', $url, $headers, $params);
~~~

自定义请求方法：

~~~php
$httpClient = new HttpClient([
    'timeout' => 10,
    'headers' => [
        'access-token' => 'ACCESS_TOKEN',
    ],
]);
$params = [
    'username' => '18600001111',
    'password' => '******',
];
$url = 'https://api.weixin.qq.com/cgi-bin/user/info/updateremark?access_token=ACCESS_TOKEN';
$httpClient->request($url, 'POST', $params);
~~~

获取请求信息：

~~~php
$requestUrl     = $httpClient->getRequestUrl();
$requestMethod  = $httpClient->getRequestMethod();
$requestHeaders = $httpClient->getRequestHeaders();
$requestBody    = $httpClient->getRequestBody();
~~~

获取响应信息：

~~~php
$error          = $httpClient->getResponseError();
$statusCode     = $httpClient->getResponseStatusCode();
$headers        = $httpClient->getResponseHeaders();
$body           = $httpClient->getResponseBody();
~~~