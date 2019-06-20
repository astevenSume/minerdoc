# REST 通用设计规则

资源：往往对应着后台系统中对象，比如一个用户User，一个商品Product，一个任务Task等等

用对应的接口表示要对资源进行何种操作，想要实现什么目的：

HTTP Verb=HTTP方法 | 操作类型=CRUD | 返回值 |
| :--- | :--- | :--- |
| POST  | Create创建 | <ul><li>正常</li><ul><li>201 (Created)</li></ul><li>异常</li><ul><li>404 (Not Found)</li><li>409 (Conflict)</li></ul>|
| GET  | Read读取 | <ul><li>正常：</li><ul><li>200 (OK)</li></ul><li>异常：</li><ul><li>404 (Not Found)</li></ul> |
| PUT  | Replace替换 | <ul><li>正常：</li><ul><li>200 (OK)</li></ul><li>异常</li><ul><li>405 (Method Not Allowed)</li><li>204 (No Content)</li><li>404 (Not Found)</li></ul> |
| PATCH  | Update/Modify更新 | <ul><li>正常：</li><ul><li>200 (OK)</li></ul><li>异常</li><ul><li>405 (Method Not Allowed)</li><li>204 (No Content)</li><li>404 (Not Found)</li></ul> |
| DELETE  | Delete删除 | <ul><li>正常：</li><ul><li>200 (OK)</li><li>204 (No Content)</li></ul><li>异常：</li><ul><li>404 (Not Found)</li><li>405 (Method Not Allowed)</li></ul> |

## 举例：RESTful的某个类似于外卖的项目的API

* 用户
    * 获取用户信息
        * `GET /v1/users/{userId}`
    * 修改用户信息
        * `PUT /v1/users/{userId}/info`
    * 修改密码
        * `PUT /v1/users/{userId}/password`
* 订单
    * 获取订单任务信息
        * `GET /v1/tasks/{taskId}/users/{userId}`
    * 发布任务
        * `POST /v1/tasks/users/{userId}`
    * 发单人确认任务信息
        * `PUT /v1/tasks/{taskId}/users/{userId}/confirmInfo`
