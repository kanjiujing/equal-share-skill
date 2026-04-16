
# equal-data-skill

## 概述

**equal-data-skill** 是基于 PyPI 包 `equal-data` 封装的金融数据服务 Skill，主要是用于查询A股股票的各个维度统计信息。该模块通过标准化API方式统一了数据资产的对外服务方式，以帮助有需要的技术用户更实时、简洁、轻量的使用相关数据。

## 快速上手

- 安装python运行环境(推荐python3.6+)，并安装equal-data依赖包。

```bash
python -m venv test_env
source test_env/bin/activate
pip install equal-data -i https://pypi.tuna.tsinghua.edu.cn/simple
```

- 根据接口文档，使用python代码获取数据。（如**高管增减持金额排行榜**接口）

```python
from equal_data import EqualDataApi
import os

# 读取环境变量中的api_key, 或者读取本地记录的api_key
api_key = os.getenv('EQUAL_DATA_API_KEY')

api = EqualDataApi(api_key)

# 高管持股变动-增减持金额排行榜列表
data = api.query_equal_data(
    interfaceId="B6",
    period=None,  # int  # 默认: 1
    changeType=None,  # int  # 默认:
    pageIndex=None,  # int  # 默认: 0
    pageSize=None,  # int  # 默认: 10
    selfSelected=None,  # bool  # 默认: false
    sortDesc=None,  # str  # 默认: 1-DESC
)
```

## 参数格式说明

| 名称           | 类型      | 必填 | 默认值   | 说明                                                         |
| :------------- | :-------- | :--- | :------- | :----------------------------------------------------------- |
| `interfaceId`  | `str`  | 是   | `B6`   | 接口ID                                                       |
| `period`       | `int` | 否   | `1`      | 1-近1月、2-近3月、3-近半年、4-近1年                          |
| `changeType`   | `int` | 否   | -        | 变动类型（增持：1，减持：-1）                                |
| `pageIndex`    | `int` | 是   | `0`      | 当前页从0开始                                                |
| `pageSize`     | `int` | 是   | `10`     | 每页显示记录数                                               |
| `selfSelected` | `bool` | 否   | `false`  | true: 只看自选 false：全部（默认）                           |
| `sortDesc`     | `str`  | 否   | `1-DESC` | 排序描述 1-ASC/1-DESC 等，1表示增持金额 2增持数量 3占总股本比 4占流通股本比 <br>5净增持股数 6增持均价 |

- 返回格式：json

## 触发指令

【A股】【股票】【行情】【K线】【股价】【涨跌幅】【成交量】【市值】
【基金】【净值】【收益率】【持仓】【基金经理】
【财报】【财务指标】【营收】【净利润】【毛利率】【资产负债】
【高管增减持】【董监高】【股东】【持股变动】【增持】【减持】
【机构动向】【机构持仓】【北向资金】【外资】【社保基金】
【龙虎榜】【游资】【营业部】【上榜】【打板】【连板】【市场高度】
【限售解禁】【解禁股】【减持计划】
【大宗交易】【折价】【溢价】
【重大合同】【涨跌概率】
【分红送转】
【机构调研】
【业绩预告】【预增】【预减】【暴雷】
【十大股东】【流通股东】【股东人数】【管理层】【高管】
【快讯】【新闻】【公告】【研报】【资讯】
【热门榜单】
