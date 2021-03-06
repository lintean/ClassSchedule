﻿# 排课demo前后端接口

标签（空格分隔）： 接口 排课

---

### 1. 用户登录

- 路径： ./api/logIn.js
- 方法： POST
- 参数： 

		form-data {
			userName: "用户名",
			password: "密码"
		}

- 返回值：

		JSON {
			code: 错误编号,
			msg: 错误信息 （无错误时可无此项）
		}

- 错误说明：

		错误码  说明
		 0      成功
		 400    链接错误
		 403    用户名或密码错误
		 409    此用户名已被占用（注册时）
		 500    服务器或数据库错误
		 
### 2. 用户注册

 - 路径：./api/register.js
 - 方法：POST
 - 参数：

        form-data{
            userName: "用户名",
			password: "密码"
        }
    
 - 返回：

		JSON {
			code: 错误编号,
			msg: 错误信息 （无错误时可无此项）
		}
		
### 3. 获取用户排课任务（登录后）

 - 路径：./api/getSchedule.js
 - 方法：GET
 - 参数：无
 - 返回：

        JSON{
            code: "错误代码"
            userName: "用户名",
            schedules[
                ｛
                scheduleName: "排课名称",
                type: "类型",
                status: "状态",
                time: "创建时间"
                ｝ * n
                //类型为云校排课上所有，如果不需要可删除
                //初定状态有“排课中”“排课完成”
            ]
        }
 - 错误代码

        错误码	说明
         0      成功
		 400    链接错误
		 403    用户未登录
		 500    服务器或数据库错误
        
### 4. 修改排课任务名称

 - 路径：./api/editScheduleName.js
 - 方法：POST
 - 参数：

        form-data{
            oldName: "需要修改的名称",
            newName: "修改后的名称"
        }

 - 返回：
 
		JSON {
			code: 错误编号,
			msg: 错误信息 （无错误时可无此项）
		}
 - 错误代码

        错误码	说明
         0      成功
		 400    链接错误
		 403    需要修改的任务不存在
		 409    修改后的名称重名
		 500    服务器或数据库错误

### 5. 删除排课任务

 - 路径：./api/deleteSchedule.js
 - 方法：POST
 - 参数：

        form-data{
            scheduleName: "任务名称"
        }
        
 - 返回：

		JSON {
			code: 错误编号,
			msg: 错误信息 （无错误时可无此项）
		}
 - 错误代码

        错误码	说明
         0      成功
		 400    链接错误
		 403    需要删除的任务不存在
		 500    服务器或数据库错误
		
### 6. 上传任课信息

 - 路径：./api/uploadExcelJson.js
 - 方法：POST
 - 参数：

        form-data{
            excel[
                {"键1":"值1","键2":"值2" * n} * m
                //n可认为是列数，m为行数
            ]
        }

 - 返回：

		JSON {
			code: 错误编号,
			msg: 错误信息 （无错误时可无此项）
		}
 - 错误代码

        错误码	说明
         0      成功
		 400    链接错误
		 403    格式错误（？需要告诉他格式有错误吗）
		 500    服务器或数据库错误
 - 示例：

```json
[
{"年级":"高二","班级":"1班","语文":"3+1","":"宁文瑞","数学":"5","":"謇梦菲","外语":"5","":"况晏然","艺术":"1","":"司马凝竹","劳技":"1","":"苟明远","体育":"3","":"宜采萱+功凌寒","班会":"1","":"裔春蕾"},
{"年级":"高二","班级":"2班","语文":"3+1","":"吕三诗","数学":"5","":"鱼志诚","外语":"5","":"同香巧","艺术":"1","":"司马凝竹","劳技":"1","":"苟明远","体育":"3","":"宜采萱+功凌寒","班会":"1","":"鱼志诚"},
{"年级":"高二","班级":"3班","语文":"3+1","":"夕自珍","数学":"5","":"呼延青香","外语":"5","":"同香巧","艺术":"1","":"司马凝竹","劳技":"1","":"苟明远","体育":"3","":"宜采萱+功凌寒","班会":"1","":"同香巧"},
{"年级":"高二","班级":"4班","语文":"3+1","":"似若华","数学":"5","":"謇梦菲","外语":"5","":"仝骏年","艺术":"1","":"司马凝竹","劳技":"1","":"苟明远","体育":"3","":"宜采萱+功凌寒","班会":"1","":"令狐春蕾"},
{"年级":"高二","班级":"5班","语文":"3+1","":"吕三诗","数学":"5","":"黎乐康","外语":"5","":"生长娟","艺术":"1","":"司马凝竹","劳技":"1","":"阳雅志","体育":"3","":"宜采萱+郁嘉禾","班会":"1","":"吕三诗"},
{"年级":"高二","班级":"6班","语文":"3+1","":"夕自珍","数学":"5","":"黎乐康","外语":"5","":"乘清妍","艺术":"1","":"司马凝竹","劳技":"1","":"阳雅志","体育":"3","":"宜采萱+郁嘉禾","班会":"1","":"夕自珍"},
{"年级":"高二","班级":"7班","语文":"3+1","":"委尔真","数学":"5","":"鱼志诚","外语":"5","":"况晏然","艺术":"1","":"司马凝竹","劳技":"1","":"偶灵凡","体育":"3","":"简凌波+郁嘉禾","班会":"1","":"委尔真"},
{"年级":"高二","班级":"8班","语文":"3+1","":"委尔真","数学":"5","":"万俟曼珍","外语":"5","":"乘清妍","艺术":"1","":"司马凝竹","劳技":"1","":"阳雅志","体育":"3","":"宜采萱+郁嘉禾","班会":"1","":"赛高逸"},
{"年级":"高二","班级":"9班","语文":"3+1","":"祈嫚儿","数学":"5","":"旅从灵","外语":"5","":"仝骏年","艺术":"1","":"司马凝竹","劳技":"1","":"阳雅志","体育":"3","":"宜采萱+郁嘉禾","班会":"1","":"碧鲁寻绿"},

]
```
  





