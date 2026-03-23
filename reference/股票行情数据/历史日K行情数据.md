# 历史日K行情数据

> 分类: 股票行情数据 | 目录: `股票行情数据` | 索引见 `SKILL.md`


### 描述

历史日K行情数据

### 请求参数

| 名称 | 类型 | 必填 | 默认值 | 说明 |
|:---|:---|:---|:---|:---|
| `interfaceId` | `String` | 是 | "42" | 接口ID |
| `stockCodeList` | `List<String>` | 否 | - | 单次查询股票代码列表（不超过50个） |

### 返回参数

ResultData.data 为 List，元素为历史日K行情列表

| 名称 | 类型 | 是否必返回 | 说明 |
|:---|:---|:---|:---|
| `stockCode` | `String` | 否 | 股票代码 |
| `stockName` | `String` | 否 | 股票名称 |
| `tradeDate` | `String` | 否 | 交易日 |
| `newPrice` | `Bigdecimal` | 否 | 最新价 |
| `maxPrice` | `Bigdecimal` | 否 | 最高价 |
| `minPrice` | `Bigdecimal` | 否 | 最低价 |
| `openPrice` | `Bigdecimal` | 否 | 开盘价 |
| `yesterdayClosePrice` | `Bigdecimal` | 否 | 昨收价 |
| `chg` | `BigDecimal` | 否 | 涨跌幅 |
| `chgMoney` | `Bigdecimal` | 否 | 涨跌额 |
| `volume` | `Long` | 否 | 成交量 |
| `tradeMoney` | `Bigdecimal` | 否 | 成交额 |

### 调用示例

```python
from equal_data import KjjApi 
api = KjjApi('bear your token') 
token = os.getenv('KJJ_API_KEY')  
# 调用接口
data = api.query_kjj_data(
    interfaceId="42",
    stockCodeList=None,  # List<String>  # 默认: 
)
```


