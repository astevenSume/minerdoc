# 服务端 - 管理员管理

## 获取菜单列表

### HTTP 请求

- GET `v1/admin/menu/getlist`

### 请求参数

> Response:

```json
{
    "code": 200,
    "data": {
        "list": [
            {
                "id": 1,
                "level": 1,
                "name": "修改后的一级菜单",
                "path": "/root/change",
                "icon": "change.jpg",
                "component": "change component",
                "order_id": 1,
                "utime": 1560744422
            },
            {
                "id": 2,
                "pid": 1,
                "level": 2,
                "name": "测试菜单2",
                "path": "/root/two",
                "component": "component",
                "order_id": 1,
                "ctime": 1560740182,
                "utime": 1560740182
            },
            {
                "id": 3,
                "pid": 1,
                "level": 2,
                "name": "测试菜单22",
                "path": "/root/two",
                "component": "component",
                "order_id": 2,
                "ctime": 1560740191,
                "utime": 1560740191
            },
            {
                "id": 4,
                "level": 1,
                "name": "第二个测试菜单",
                "path": "/root/two",
                "icon": "test2.jpg",
                "component": "component",
                "order_id": 2,
                "ctime": 1560740227,
                "utime": 1560740227
            },
            {
                "id": 6,
                "pid": 4,
                "level": 2,
                "name": "第二个测试菜1单",
                "path": "/root/two",
                "component": "component",
                "order_id": 1,
                "ctime": 1560740297,
                "utime": 1560740297
            },
            {
                "id": 7,
                "pid": 4,
                "level": 2,
                "name": "第二个测试菜2单",
                "path": "/root/two",
                "component": "component",
                "order_id": 2,
                "ctime": 1560740305,
                "utime": 1560740305
            }
        ],
        "meta": {
            "limit": 100,
            "page": 1,
            "total": 6
        }
    }
}
```

### 响应数据

| 字段名称       | 是否必须 | 类型   | 描述          | 取值范围 |
| ------------- | ------- | ------ | ------------ | ------- |
| id            | true    | int    | 菜单id |         |
| pid       | true    | int | 父菜单id |         |
| level | true    | string | 菜单等级                              |         |
| path | true    | int    | 角色id        |         |
| component | true    | int    | 管理员状态     |  |
| order_id | true    | string | 排序id       |         |
| ctime         | false   | long   | 创建时间  |         |
| utime         | false   | long   | 更新时间  |         |
| name | true | string | 菜单名字 | |
| icon | true | string | 图标 | |
| hide_in_menu | true | bool | 是否隐藏，如果是false的话没有这个字段 | |



## 创建菜单

### HTTP 请求

- POST `v1/admin/menu/add`

```json
{
	"pid":0,
	"level":1,
	"name":"测试菜单",
	"path":"/root/two",
	"icon":"test.jpg",
	"hide_in_menu":false,
	"component":"component",
	"order_id":1
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述       |
| ------------ | -------- | ------ | ------ | ---------- |
| pid          | true     | int    | NA     | 父菜单的id |
| level        | true     | int    | NA     | 菜单等级,一级菜单的等级是1,如果没有等级为1的菜单，将会没有数据   |
| name         | true     | string | NA     | 菜单名字   |
| path         | true     | string | NA     | 路径       |
| icon         | true     | string | NA     | 菜单图标   |
| hide_in_menu | true     | bool   | NA     | 是否隐藏   |
| component    | true     | string | NA     | 组件       |
| order_id     | true     | int    | NA     | 排序顺序,order_id要从1开始,不能出现0   |

> Response:

```json
{"code":200}
```

### 响应数据
增加成功返回成功状态码

## 删除菜单

### HTTP 请求

- DELETE `v1/admin/menu/del`

```json
{
"id":1
}
```

### 请求参数

| 参数名称      | 是否必须 | 类型   | 默认值   | 描述 
| ------------ | ------- | ------ | ------- | -----------
| id           | true    | int    | NA      | 菜单id,会删除这个id的菜单和其子菜单

> Response:

```json
 {"code":200}
```

### 响应数据
成功的话返回成功状态码

## 更新菜单

### HTTP 请求

- PUT `v1/admin/menu/updatemenu

```json
{
	"menus":[
	{
		"id":8,
		"pid":2,
		"level":2,
		"name":"修改后的二级菜单3",
		"path":"/root/change",
		"icon":"",
		"hide_in_menu":false,
		"component":"change component",
		"order_id":3
	},
	{
		"id":1,
		"pid":0,
		"level":1,
		"name":"修改后的一级菜单",
		"path":"/root/change",
		"icon":"change.jpg",
		"hide_in_menu":false,
		"component":"change component",
		"order_id":1
	}
]
}
```

### 请求参数

| 参数名称     | 是否必须 | 类型   | 默认值 | 描述       |
| ------------ | -------- | ------ | ------ | ---------- |
| pid          | true     | int    | NA     | 父菜单的id |
| level        | true     | int    | NA     | 菜单等级   |
| name         | true     | string | NA     | 菜单名字   |
| path         | true     | string | NA     | 路径       |
| icon         | true     | string | NA     | 菜单图标   |
| hide_in_menu | true     | bool   | NA     | 是否隐藏   |
| component    | true     | string | NA     | 组件       |
| order_id     | true     | int    | NA     | 排序顺序   |

> Response:

```json
 {"code":200}
```

### 响应数据

成功的话返回成功状态码



## 增加和更新角色菜单权限

### HTTP 请求

- POST `v1/admin/menu/updatemenuaccess`

```json
{
	"role_id":1,
	"menus_id":
		[
			1,
			2,
			3,
			4,
			5,
			6,
			7,
			8
		]
}
```

### 请求参数

| 参数名称 | 是否必须 | 类型  | 默认值 | 描述       |
| -------- | -------- | ----- | ------ | ---------- |
| role_id  | true     | int   | NA     | 父菜单的id |
| menus_id | true     | []int | NA     | 菜单id列表 |

> Response:

```json
 {"code":200}
```

### 响应数据

成功的话返回成功状态码



## 获取属于这个角色的菜单

### HTTP 请求

- GET `v1/admin/menu/getaccesslist

```json
{
	"role_id":1
}
```

### 请求参数

| 参数名称 | 是否必须 | 类型 | 默认值 | 描述   |
| -------- | -------- | ---- | ------ | ------ |
| role_id  | true     | int  | NA     | 角色id |

> Response:

```json
{
    "code": 200,
    "data": {
        "routes": [
            {
                "id": 1,
                "pid": 0,
                "hideInMenu": false,
                "path": "/root/change",
                "name": "修改后的一级菜单",
                "component": "change component",
                "icon": "change.jpg",
                "routes": [
                    {
                        "id": 3,
                        "pid": 1,
                        "hideInMenu": false,
                        "path": "/root/two",
                        "name": "测试菜单22",
                        "component": "component",
                        "icon": ""
                    },
                    {
                        "id": 2,
                        "pid": 1,
                        "hideInMenu": false,
                        "path": "/root/two",
                        "name": "测试菜单2",
                        "component": "component",
                        "icon": ""
                    }
                ]
            },
            {
                "id": 4,
                "pid": 0,
                "hideInMenu": false,
                "path": "/root/two",
                "name": "第二个测试菜单",
                "component": "component",
                "icon": "test2.jpg",
                "routes": [
                    {
                        "id": 6,
                        "pid": 4,
                        "hideInMenu": false,
                        "path": "/root/two",
                        "name": "第二个测试菜1单",
                        "component": "component",
                        "icon": ""
                    },
                    {
                        "id": 7,
                        "pid": 4,
                        "hideInMenu": false,
                        "path": "/root/two",
                        "name": "第二个测试菜2单",
                        "component": "component",
                        "icon": ""
                    }
                ]
            }
        ]
    }
}
```

### 响应数据

### 

| 参数名称     | 类型   | 默认值 | 描述                       |
| ------------ | ------ | ------ | -------------------------- |
| pid          | int    | NA     | 父菜单的id                 |
| level        | int    | NA     | 菜单等级                   |
| name         | string | NA     | 菜单名字                   |
| path         | string | NA     | 路径                       |
| icon         | string | NA     | 菜单图标                   |
| hide_in_menu | bool   | NA     | 是否隐藏                   |
| component    | string | NA     | 组件                       |
| order_id     | int    | NA     | 排序顺序                   |
| routes       | 数组   | NA     | 一级菜单包含的二级菜单数组 |

