# Equal-data

## 概述

equal-data是一个财经数据接口包，主要是用于查询A股股票的每日成交价格。该模块通过标准化API方式统一了数据资产的对外服务方式，以帮助有需要的技术用户更实时、简洁、轻量的使用相关数据。

## 快速上手

- 安装python运行环境(推荐python3.7+)，并安装tushare依赖包(推荐从清华pypi镜像安装)。

```bash
pip install equal-data -i https://pypi.tuna.tsinghua.edu.cn/simple
```

- 根据接口文档，使用python代码获取数据。（如**高管增减持金额排行榜**接口）

```python
from kjj import KjjApi

api = KjjApi('bear your token')

# 高管持股变动-增减持金额排行榜列表
data = api.query_kjj_data(
    interfaceId="14",
    period=None,  # Integer  # 默认: 1
    changeType=None,  # Integer  # 默认: 
    pageIndex=None,  # Integer  # 默认: 0
    pageSize=None,  # Integer  # 默认: 10
    selfSelected=None,  # boolean  # 默认: false
    sortDesc=None,  # String  # 默认: 1-DESC
)
```

## 参数格式说明



- | 名称           | 类型      | 必填 | 默认值   | 说明                                                         |
  | :------------- | :-------- | :--- | :------- | :----------------------------------------------------------- |
  | `interfaceId`  | `String`  | 是   | `14`     | 接口ID                                                       |
  | `period`       | `Integer` | 否   | `1`      | 1-近1月、2-近3月、3-近半年、4-近1年                          |
  | `changeType`   | `Integer` | 否   | -        | 变动类型（增持：1，减持：-1）                                |
  | `pageIndex`    | `Integer` | 是   | `0`      | 当前页从0开始                                                |
  | `pageSize`     | `Integer` | 是   | `10`     | 每页显示记录数                                               |
  | `selfSelected` | `boolean` | 否   | `false`  | true: 只看自选 false：全部（默认）                           |
  | `sortDesc`     | `String`  | 否   | `1-DESC` | 排序描述 1-ASC/1-DESC 等，1表示增持金额 2增持数量 3占总股本比 4占流通股本比 <br>5净增持股数 6增持均价 |

- 返回格式：json

## 功能

调用 equal-data PyPI 包获取历史数据。

## 使用方式

当用户需要获取历史数据时，使用此 Skill。

## 触发指令

- "看究竟API"
- “高管持股变动”
- “机构动向/机构跟踪/机构风云榜”
- “龙虎榜”
- “营业部交易数据”
- "看究竟的交易策略"
