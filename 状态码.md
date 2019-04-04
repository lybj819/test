# **API接口 返回错误码**
|宏定义	|错误码	|错误描述	| 一般措施|
|-------|-------|--------|-------|
|LINK_NO_MEMORY	|-1000 |内存申请错误 | 内存不足，通常由于机器内存不足或者程序内存回收存在问题。措施：检查代码逻辑包括上传 sdk 和用户代码|
|	LINK_MUTEX_ERROR|-1100	|线程互斥锁错误	| 程序内部同步调用失败，通常由于内存越界或者对未初始化或者已销毁的锁或条件变量进行了操作。 措施：检查代码逻辑包括上传sdk和用户代码|
|LINK_COND_ERROR	|-1101	|线程条件变量错误	| 程序内部同步调用失败，通常由于内存越界或者对未初始化或者已销毁的锁或条件变量进行了操作。 措施：检查代码逻辑包括上传sdk和用户代码|
|LINK_THREAD_ERROR	|-1102	|线程错误	| 创建上传线程失败，通常由于资源不足造成。 措施：内存溢出，需要检查代码包括上传 sdk 和用户代码|
|LINK_TIMEOUT|-2000|超时||
|LINK_NO_PUSH	|-2001	|队列不允许推送数据	| 程序内部发生了逻辑错误。 措施：需要详细 log 并[提交工单](https://support.qiniu.com/tickets/category?ref=developer.qiniu.com)|
|LINK_BUFFER_IS_SMALL	|-2003	|缓存太小| 提供的 buffer 缓冲太小。 措施：增大提供缓冲的大小|
|LINK_ARG_TOO_LONG|-2004| 参数太长	| deviceid(ua name) 长度超长了。 措施：检查输入参数|
|LINK_ARG_ERROR	|-2100	|参数错误	| 传参不正确。 措施：检查输入参数|
|LINK_JSON_FORMAT	|-2200	|JSON数据格式错误| 服务器返回数据包错误。 措施：需要详细 log 并[提交工单](https://support.qiniu.com/tickets/category?ref=developer.qiniu.com)|
|LINK_HTTP_TIME	|-2300	|获取时间出错	| 措施：检查本地网络|
|LINK_Q_OVERWRIT|-5001	|队列数据被覆盖	| 通常是1. 网络太慢 2. 缓存 buffer 设置的太小。 措施：1. 检查本地网络带宽，2. 按流媒体码率大小，正确配置缓存 buffer|
|LINK_Q_WRONGSTATE|-5002 |队列状态错误 |1|
|LINK_MAX_SEG|-5103|片段处理到达最大值||
|LINK_NOT_INITED|-5104|操作对象未初始化||
|LINK_MAX_CACHE|-5105|缓存到达最大值||
|LINK_Q_OVERFLOW|-5005|队列数据溢出||
|LINK_PAUSED|-6000|暂停状态||
|LINK_GHTTP_FAIL|-7000|http请求失败||
|LINK_SUCCESS|0|返回成功||
|LINK_ERROR|-1|返回失败|1|


#  **异步错误**
在api接口调用成功但是却发现没有上传文件时候就需要检查日志以确定失败原因，日志以标准输出的方式输出至控制台：

|错误描述	| 日志|
|--------|-------|
|token 过期	| upload file :ts/testuid3/testdeviceid/2018/08/21/14/11/50/021/1534831910693/7.ts errorcode=401 errmsg={"error":"expired token"}|
|token 错误	| upload file :ts/testuid3/testdeviceid/2018/08/21/14/14/37/809/1534832077481/7.ts errorcode=401 errmsg={"error":"bad token"}|
|服务端无响应	|upload file :ts/testuid3/testdeviceid/2018/08/21/14/11/50/021/1534831910693/7.ts errorcode=52 errmsg={"error":"server not response"}|
|上传回调出错	|upload file :ts_testuid3_testdeviceid_2018_08/21/14/16/51/223_1534832211895/7.ts errorcode=579 errmsg={"error": "callback error: bad file name"}|
|上传超时	| upload file :ts/ipcxxa/1538122486432/1538122486432/7.ts expsize:260568 errorcode=52 errmsg={"error":"the operation was aborted by an application callback"}|


*注：上传是异步上传的，需要查日志确认失败原因*
