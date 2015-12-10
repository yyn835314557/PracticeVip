# 有关验签的API

- sending and Signing [Requests]()
	- requeset 必须带有如下3个参数
		- api_key 表示应用的API
		- timestamp 单位为秒必须在8小时之内
		- api_sign 签名必须通过 HTTP Authorization header传输

- Signature Generation
	- `signature = SHA1(secret,base string)`
		- SHA1: hash algorithm
			- secret
				- If user token is not present in request, then secret=API secret; if user token is present in request,then secret=API secret&toke n secret
				- Secret is added to the very beginning of the base string, this will achieve better security
			- base string
				- Parameters are sorted by their names' alphabetic order
				- Parameter with empty key (null, "") is always ignored
				- Parameter with whitespace key (" ") is preserved
				- Parameter with empty value is always ignored
				- Parameter with whitespace value is preserved
				- Parameter with multiple identical keys (warehouse=xxx&warehouse=yyy), only the first entry is preserved 
- Response: API response
	- code: 成功或者失败的响应码
	- msg: 响应消息
	- data: 响应结果

	```
	{
		"code": 1,
		"msg": "success", 
		"data": {
		"tokenId": "BE7E1857637EA5481DA4451858EB4DEF299A0E2B", 
		"tokenSecret": "1D7FB177CA5408740841CB67AB3D1A07", 
		"userId": 65704503
		} 
	}
	```

	- Response code:
		- 1: 成功
		- 2: 成功(有警告)
		- 10000: mapi异常
		- 10001: 输入参数引起异常
		- 11000: authentication failure，App重定向到登录页面
		- 12000: API引起的异常
		- 13000: 用户相关异常
		- 13001: 用户以存在异常
		- 14000: 购物车相关异常
