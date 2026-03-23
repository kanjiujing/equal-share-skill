# ST股票列表

> 分类: 股票基础数据 | 目录: `股票相关数据` | 索引见 `SKILL.md`


### 描述

获取ST股票列表

### 请求参数

| 名称 | 类型 | 必填 | 默认值 | 说明 |
|:---|:---|:---|:---|:---|
| `interfaceId` | `String` | 是 | "4" | 接口ID |
| `pageNum` | `Integer` | 否 | `0` | 分页偏移量，从 0 开始（第 1 页为 0，第 2 页为 pageSize） |
| `pageSize` | `Integer` | 否 | `10` | 每页条数 |
| `stockList` | `List<String>` | 否 | - | 股票代码/名称,如果传递的股票不是ST，会返回空列表 |

### 返回参数

ResultData.data 为 List，元素为ST股票

| 名称 | 类型 | 是否必返回 | 说明 |
|:---|:---|:---|:---|
| `data` | `List<ListedCompanyVo>` | 否 | ST股票列表 |
| `stockCode` | `String` | 否 | 股票代码 |
| `companyName` | `String` | 否 | 公司全称 |
| `companyShortName` | `String` | 否 | 公司简称 |
| `formername` | `String` | 否 | 曾用名 |
| `industry` | `String` | 否 | 所属行业 |
| `subIndustry` | `String` | 否 | 所属子行业 |
| `establishmentDate` | `String` | 否 | 成立日期 |
| `registrationDate` | `String` | 否 | 注册日期 |
| `registeredCapital` | `String` | 否 | 注册资金（亿） |
| `province` | `String` | 否 | 所属地域 |
| `registeredProvince` | `String` | 否 | 注册地点省 |
| `registeredCity` | `String` | 否 | 注册地点市 |
| `registeredCounty` | `String` | 否 | 注册地点县 |
| `legalRepresentative` | `String` | 否 | 法人代表 |
| `listingDate` | `String` | 否 | 上市时间 |
| `companyType` | `String` | 否 | 公司类型 |
| `businessOverview` | `String` | 否 | 业务概述 |
| `actualController` | `String` | 否 | 实际控制人 |
| `companyIntroduction` | `String` | 否 | 公司简介 |
| `businessRegistrationNumber` | `String` | 否 | 工商注册号 |
| `industryDomain` | `String` | 否 | 行业领域 |
| `stockType` | `String` | 否 | 证券类别 |
| `businessScope` | `String` | 否 | 经营范围 |
| `delistedDate` | `Date` | 否 | 退市时间 |

### 调用示例

```python
from kjj import KjjApi 
api = KjjApi('bear your token') 

# 调用接口
data = api.query_kjj_data(
    interfaceId="4",
    pageNum=None,  # Integer  # 默认: 0
    pageSize=None,  # Integer  # 默认: 10
    stockList=None,  # List<String>  # 默认: 
)
```


