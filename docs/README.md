# 上海公交 API

### 主页（页面）

```
https://shanghaicity.openservice.kankanews.com/
```

### 公交实时到站（页面）

```
https://shanghaicity.openservice.kankanews.com/public/bus
```

#### 查询公交线路编号 API

把公交线路名称转换成公交线路唯一标识符，方便接下来的查询操作

```
POST https://shanghaicity.openservice.kankanews.com/public/bus/get      
```

请求参数

|  参数名   | 可选  | 含义 |
|  ----  | ----  | ---- |
| idnum  | 必选 | 公交线路完整名称，如：闵行15路


返回响应（application/json）

|  参数名   | 可选  | 含义 |
|  ----  | ----  | ---- |
| sid  | 必选 | String，公交线路唯一标识符，将用于接下来的查询
| mes | 不明 |String， 不明 |

#### 查询公交线路详情（页面）

根据公交线路唯一标识查询其上下行和途径站点信息

```
POST https://shanghaicity.openservice.kankanews.com/public/bus/mes/sid/${sid}      
```

请求参数

|  参数名   | 可选  | 含义 |
|  ----  | ----  | ---- |
| stoptype  | 可选 | 公交线路方向，取值范围 { 0, 1}，默认 0
| ${sid}  | 必选 |  公交线路唯一标识符，参考 *查询公交线路编号 API* 接口


返回响应（text/html）

响应是一个 HTML 页面，包括两类信息：

**方向信息**
公交线路上下行起点和终点站名称，首末班车时间

**途径站点信息**
站点名称和站点编号信息

#### 查询实时到站信息 API

根据公交线路和站点以及方向，查询下一班车到站信息

```
POST https://shanghaicity.openservice.kankanews.com/public/bus/Getstop      
```

请求参数

|  参数名   | 可选  | 含义 |
|  ----  | ----  | ---- |
| sid  | 必选 | 公交线路唯一标识符
| stopid  | 必选 | 途径站点编号信息， *查询公交线路详情* 页面可以查询到该编号
| stoptype | 必选 | 公交车辆运行方向，取值范围 { 0, 1}，默认 0

返回响应（application/json）

|  参数名   | 可选  | 含义 |
|  ----  | ----  | ---- |
| @attributes.cod  | 必选 | String，公交线路名称
| distance | 必选 | String，下一班公交车距离本站还有多少米 |
| stopdis | 必选 | String，下一班公交车距离本站还有多少站 |
| terminal | 必选 | String，下一班公交车车牌号 |
| time | 必选 | String，下一班公交车预计还有多少秒到达本站，这个字段也有可能是 `xxx分钟` 格式 |
