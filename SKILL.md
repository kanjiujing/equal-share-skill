---
name: equal-data-skill
description: 看究竟金融数据服务 Skill - 提供 A 股行情、基金、财报、高管增减持、机构动向、龙虎榜、基金画像等专业金融数据查询
author: 看究竟
pypi_package: equal-data
install_required: true
install_command: pip install equal-data==0.0.4
required_env_vars:
  - KJJ_API_TOKEN
---

# equal-data

## 概述

equal-data是一个财经数据接口包，主要是用于查询A股股票的每日成交价格。该模块通过标准化API方式统一了数据资产的对外服务方式，以帮助有需要的技术用户更实时、简洁、轻量的使用相关数据。

## 快速上手

- 安装python运行环境(推荐python3.6+)，并安装equal-data依赖包。

```bash
python -m venv test_env
source test_env/bin/activate
pip install equal-data -i https://pypi.tuna.tsinghua.edu.cn/simple
```

- 根据接口文档，使用python代码获取数据。（如**高管增减持金额排行榜**接口）

```python
from kjj import KjjApi
import os

# 读取环境变量中的token, 或者读取本地记录的token
token = os.getenv('KJJ_API_TOKEN')

api = KjjApi(token)

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

| 名称           | 类型      | 必填 | 默认值   | 说明                                                         |
| :------------- | :-------- | :--- | :------- | :----------------------------------------------------------- |
| `interfaceId`  | `String`  | 是   | `14`     | 接口ID                                                       |
| `period`       | `Integer` | 否   | `1`      | 1-近1月、2-近3月、3-近半年、4-近1年                          |
| `changeType`   | `Integer` | 否   | -        | 变动类型（增持：1，减持：-1）                                |
| `pageIndex`    | `Integer` | 是   | `0`      | 当前页从0开始                                                |
| `pageSize`     | `Integer` | 是   | `10`     | 每页显示记录数                                               |
| `selfSelected` | `boolean` | 否   | `false`  | true: 只看自选 false：全部（默认）                           |
| `sortDesc`     | `String`  | 否   | `1-DESC` | 排序描述 1-ASC/1-DESC 等，1表示增持金额 2增持数量 3占总股本比 4占流通股本比 <br>5净增持股数 6增持均价 |

- 返回格式：json

## 认证方式

本 Skill 需要看究竟 API Token (`KJJ_API_TOKEN`)，支持以下两种方式配置：

看究竟官网注册，获取token，

**方式 B：配置环境变量**。

```bash
export KJJ_API_TOKEN="your_key_here"
```

**方式 C：OpenClaw配置文件:
在 `~/.openclaw/openclaw.json` 中配置：
```json
{
  "skills": {
    "equal-data-skill": {
      "KJJ_API_TOKEN": "your_token_here"
    }
  }
}
```

## 触发指令

财务指标、主营业务
股票列表、交易日、更名、ST、行业板块、概念板块
龙虎榜、游资、营业部、市场高度
高管增减持、高管增持、高管减持
机构动向、机构持仓、机构风云榜
限售解禁
大宗交易
业绩预告、重大合同、分红、机构调研
十大股东、管理层、高管、股东人数
快讯、文章、公告

## 数据接口列表


| 接口ID | 接口名称 | 分类 | 文档路径 |
|:---:|:---|:---|:---|
| FINANCE_INDEX_MAJOR_INDICATORS_BDA2853F | 主要财务指标 | 财务指标相关数据 | [主要财务指标.md](<reference/财务指标相关数据/主要财务指标.md>) |
| FINANCE_INDEX_BUSINESS_ANALYSIS_HISTORY_DATA_A113AD31 | 主营业务数据分析历史数据 | 财务指标相关数据 | [主营业务数据分析历史数据.md](<reference/财务指标相关数据/主营业务数据分析历史数据.md>) |
| STOCK_LIST_976A0399 | 基本股票列表/公司信息 | 股票基础数据 | [基本股票列表_公司信息.md](<reference/股票基础数据/基本股票列表_公司信息.md>) |
| STOCK_TRADE_DATE_LIST_A691BBFA | 交易日期列表 | 股票基础数据 | [交易日期列表.md](<reference/股票基础数据/交易日期列表.md>) |
| STOCK_CHANGE_NAME_LIST_6C169374 | 股票更名列表 | 股票基础数据 | [股票更名列表.md](<reference/股票基础数据/股票更名列表.md>) |
| STOCK_ST_LIST_D9254E18 | ST股票列表 | 股票基础数据 | [ST股票列表.md](<reference/股票基础数据/ST股票列表.md>) |
| STOCK_HOT_INDUSTRY_STOCK_LIST_690C1159 | 热门行业板块-股票列表 | 股票基础数据 | [热门行业板块-股票列表.md](<reference/股票基础数据/热门行业板块-股票列表.md>) |
| STOCK_HOT_THEME_STOCK_LIST_21FB8583 | 热门概念板块-股票列表 | 股票基础数据 | [热门概念板块-股票列表.md](<reference/股票基础数据/热门概念板块-股票列表.md>) |
| DRAGON_TIGER_WIN_RATE_RANK_1AFFA65 | 龙虎榜-收率排行榜近1月 | 究竟特色数据专题 | [龙虎榜-收率排行榜近1月.md](<reference/究竟特色数据专题/龙虎榜-收率排行榜近1月.md>) |
| DRAGON_TIGER_STOCK_TRADEDATE_RANK_668D1998 | 龙虎榜单-个股榜 | 究竟特色数据专题 | [龙虎榜单-个股榜.md](<reference/究竟特色数据专题/龙虎榜单-个股榜.md>) |
| DRAGON_TIGER_HOT_MONEY_TRADEDATE_RANK_CBDEEFE9 | 龙虎榜-游资榜 | 究竟特色数据专题 | [龙虎榜-游资榜.md](<reference/究竟特色数据专题/龙虎榜-游资榜.md>) |
| DRAGON_TIGER_DEPT_TRADEDATE_RANK_5F3249C0 | 龙虎榜-营业部榜 | 究竟特色数据专题 | [龙虎榜-营业部榜.md](<reference/究竟特色数据专题/龙虎榜-营业部榜.md>) |
| DRAGON_TIGER_MARKET_HIGH_TRADEDATE_RANK_55B4FB4 | 龙虎榜-市场高度 | 究竟特色数据专题 | [龙虎榜-市场高度.md](<reference/究竟特色数据专题/龙虎榜-市场高度.md>) |
| DRAGON_TIGER_MANAGER_HOLDING_RANK_322EC0A8 | 高管持股-增减持变动排行榜 | 究竟特色数据专题 | [高管持股-增减持变动排行榜.md](<reference/究竟特色数据专题/高管持股-增减持变动排行榜.md>) |
| DRAGON_TIGER_MANAGER_HOLDING_CHANGE_LIST_E8127FAB | 高管持股-增减持变动明细列表 | 究竟特色数据专题 | [高管持股-增减持变动明细列表.md](<reference/究竟特色数据专题/高管持股-增减持变动明细列表.md>) |
| DRAGON_TIGER_MANAGER_HOLDING_PLAN_LIST_1AF0B10B | 高管持股-增减持计划列表 | 究竟特色数据专题 | [高管持股-增减持计划列表.md](<reference/究竟特色数据专题/高管持股-增减持计划列表.md>) |
| DRAGON_TIGER_MANAGER_HOLDING_STOCKCODE_OPT_DETAIL_D294B48C | 高管持股-增减持操作明细数据 | 究竟特色数据专题 | [高管持股-增减持操作明细数据.md](<reference/究竟特色数据专题/高管持股-增减持操作明细数据.md>) |
| DRAGON_TIGER_MANAGER_HOLDING_STOCKCODE_PLAN_DETAIL_B5554323 | 高管持股-增减持计划详情 | 究竟特色数据专题 | [高管持股-增减持计划详情.md](<reference/究竟特色数据专题/高管持股-增减持计划详情.md>) |
| DRAGON_TIGER_MANAGER_HOLDING_STOCKCODE_BASIC_INFO_937D50E | 高管持股-详情页基本信息（含数据分析） | 究竟特色数据专题 | [高管持股-详情页基本信息（含数据分析）.md](<reference/究竟特色数据专题/高管持股-详情页基本信息（含数据分析）.md>) |
| DRAGON_TIGER_AGENCY_PAGE_LIST_V250_97962782 | 机构动向-机构动向列表 | 究竟特色数据专题 | [机构动向-机构动向列表.md](<reference/究竟特色数据专题/机构动向-机构动向列表.md>) |
| DRAGON_TIGER_AGENCY_BASIC_INFO_V250_829F10F3 | 机构风云榜-榜单列表 | 究竟特色数据专题 | [机构风云榜-榜单列表.md](<reference/究竟特色数据专题/机构风云榜-榜单列表.md>) |
| DRAGON_TIGER_AGENCY_RANK_LIST_V250_B927F2B8 | 机构风云榜-榜单详情数据 | 究竟特色数据专题 | [机构风云榜-榜单详情数据.md](<reference/究竟特色数据专题/机构风云榜-榜单详情数据.md>) |
| DRAGON_TIGER_AGENCY_HOLDER_STOCK_LIST_986A9741 | 机构动向-机构持仓列表 | 究竟特色数据专题 | [机构动向-机构持仓列表.md](<reference/究竟特色数据专题/机构动向-机构持仓列表.md>) |
| DRAGON_TIGER_AGENCY_DETAIL_400A302A | 机构动向-机构详情 | 究竟特色数据专题 | [机构动向-机构详情.md](<reference/究竟特色数据专题/机构动向-机构详情.md>) |
| DRAGON_TIGER_AGENCY_CURRENT_LIST_9D50A506 | 机构动向-机构本期持股列表 | 究竟特色数据专题 | [机构动向-机构本期持股列表.md](<reference/究竟特色数据专题/机构动向-机构本期持股列表.md>) |
| DRAGON_TIGER_FREE_BATCH_LIST_FB76F3D6 | 限售解禁-解禁数据列表（历史解禁/预告/仅自选） | 究竟特色数据专题 | [限售解禁-解禁数据列表（历史解禁_预告_仅自选）.md](<reference/究竟特色数据专题/限售解禁-解禁数据列表（历史解禁_预告_仅自选）.md>) |
| DRAGON_TIGER_FREE_BATCH_STOCKCODE_DETAIL_1CA5561F | 限售解禁详情页 | 究竟特色数据专题 | [限售解禁详情页.md](<reference/究竟特色数据专题/限售解禁详情页.md>) |
| DRAGON_TIGER_FREE_BATCH_STOCKCODE_ANALYSIS_D5B7BAB8 | 限售解禁数据分析接口 | 究竟特色数据专题 | [限售解禁数据分析接口.md](<reference/究竟特色数据专题/限售解禁数据分析接口.md>) |
| DRAGON_TIGER_BULK_DATA_ACTIVE_DEPT_LIST_37C4AE61 | 大宗数据-活跃营业部 | 究竟特色数据专题 | [大宗数据-活跃营业部.md](<reference/究竟特色数据专题/大宗数据-活跃营业部.md>) |
| DRAGON_TIGER_BULK_DATA_ACTIVE_STOCK_LIST_2477A81C | 大宗数据-活跃个股 | 究竟特色数据专题 | [大宗数据-活跃个股.md](<reference/究竟特色数据专题/大宗数据-活跃个股.md>) |
| DRAGON_TIGER_PERFORMANCE_THUNDERSTORM_A138D59 | 业绩预告-业绩暴雷、业绩预增 | 究竟特色数据专题 | [业绩预告-业绩暴雷、业绩预增.md](<reference/究竟特色数据专题/业绩预告-业绩暴雷、业绩预增.md>) |
| DRAGON_TIGER_BIG_CONTRACT_LIST_3C04CC28 | 重大合同-数据列表 | 究竟特色数据专题 | [重大合同-数据列表.md](<reference/究竟特色数据专题/重大合同-数据列表.md>) |
| DRAGON_TIGER_BONUS_LIST_CE25AB7E | 分红送转-预案/实施 | 究竟特色数据专题 | [分红送转-预案_实施.md](<reference/究竟特色数据专题/分红送转-预案_实施.md>) |
| DRAGON_TIGER_AGENCY_RESEARCH_LIST_BD40F7FC | 机构调研列表 | 究竟特色数据专题 | [机构调研列表.md](<reference/究竟特色数据专题/机构调研列表.md>) |
| DRAGON_TIGER_DATE_LIST_B10D430C | 龙虎榜日期列表 | 龙虎榜 | [龙虎榜日期列表.md](<reference/打板专题数据/龙虎榜日期列表.md>) |
| DRAGON_TIGER_DEPT_BELONG_HOT_MONEY_8CF53BF9 | 龙虎榜机构（营业部）-所属游资席位 | 打板专题数据 | [龙虎榜机构（营业部）-所属游资席位.md](<reference/打板专题数据/龙虎榜机构（营业部）-所属游资席位.md>) |
| DRAGON_TIGER_DEPT_HOLDING_DETIAL_LIST_F4578FA0 | 龙虎榜机构（营业部）-操作明细 | 打板专题数据 | [龙虎榜机构（营业部）-操作明细.md](<reference/打板专题数据/龙虎榜机构（营业部）-操作明细.md>) |
| DRAGON_TIGER_DETAIL_HOTMONEY_ANALYSIS_FBB71945 | 龙虎榜-游资特色指标分析（近1年/近1月） | 打板专题数据 | [龙虎榜-游资特色指标分析（近1年_近1月）.md](<reference/打板专题数据/龙虎榜-游资特色指标分析（近1年_近1月）.md>) |
| DRAGON_TIGER_HOT_MONEY_DTL249_B4962607 | 游资基本信息 | 打板专题数据 | [游资基本信息.md](<reference/打板专题数据/游资基本信息.md>) |
| DRAGON_TIGER_HOT_MONEY_OPT_BF4B9B9B | 游资-每日操作明细 | 打板专题数据 | [游资-每日操作明细.md](<reference/打板专题数据/游资-每日操作明细.md>) |
| STOCK_QUOTE_REAL_TIME_QUOTE_LIST_3E577EB | 实时行情列表 | 股票行情数据 | [实时行情列表.md](<reference/股票行情数据/实时行情列表.md>) |
| STOCK_QUOTE_HISTORY_QUOTE_LIST_C82F9954 | 历史日K行情数据 | 股票行情数据 | [历史日K行情数据.md](<reference/股票行情数据/历史日K行情数据.md>) |
| LISTEDCOMPANY_MANAGER_LIST_FF45CB43 | 上市公司管理层信息 | 上市公司股东数据 | [上市公司管理层信息.md](<reference/上市公司股东数据/上市公司管理层信息.md>) |
| LISTEDCOMPANY_TEN_SHAREHOLDER_LIST_75B38FFF | 十大股东/十大流通股东 | 上市公司股东数据 | [十大股东_十大流通股东.md](<reference/上市公司股东数据/十大股东_十大流通股东.md>) |
| LISTEDCOMPANY_HOLDER_NUM_6ED90164 | 股东人数列表数据 | 上市公司股东数据 | [股东人数列表数据.md](<reference/上市公司股东数据/股东人数列表数据.md>) |
| LISTEDCOMPANY_INSTITUTION_HOLDING_DETAIL_DBC4812E | 公司详情页-股东股本 -机构持仓明细 | 上市公司股东数据 | [公司详情页-股东股本_-机构持仓明细.md](<reference/上市公司股东数据/公司详情页-股东股本_-机构持仓明细.md>) |
| LISTEDCOMPANY_LATEST_FINANCE_INDEX_4A98062C | 公司详情页-最新一期指标展示 | 上市公司股东数据 | [公司详情页-最新一期指标展示.md](<reference/上市公司股东数据/公司详情页-最新一期指标展示.md>) |
| NEWS_INFO_NEWS_LIST_530922EB | 快讯信息（近一个月的快讯） | 资讯信息 | [快讯信息（近一个月的快讯）.md](<reference/资讯信息/快讯信息（近一个月的快讯）.md>) |
| NEWS_INFO_ARTICLE_LIST_D6DA008D | 文章信息 | 资讯信息 | [文章信息.md](<reference/资讯信息/文章信息.md>) |
| NEWS_INFO_NOTICE_ANNOUNCEMENT_LIST_53A04ED2 | 公告信息 | 资讯信息 | [公告信息.md](<reference/资讯信息/公告信息.md>) |

## 分类统计

| 分类 | 接口数量 |
|:---|:---|
| 财务指标相关数据 | 2 |
| 股票基础数据 | 6 |
| 究竟特色数据专题 | 26 |
| 龙虎榜 | 1 |
| 打板专题数据 | 5 |
| 股票行情数据 | 2 |
| 上市公司股东数据 | 5 |
| 资讯信息 | 3 |
| **合计** | **50** |

## 数据来源与依赖
- **API 提供商**: 看究竟(kjiujing.com)
- **官方文档**: `https://api.kjiujing.com/docs`
- **PYPI包地址**: `https://pypi.org/project/equal-data/`
- **看究竟官网**: `[https://www.kjiujing.com](https://www.kjiujing.com/)`
- **数据用途**: 仅用于获取行情数据，不涉及交易操作
- **开源依赖**:
  - requests (Apache 2.0)
  - pandas (BSD 3-Clause)
  - equal-data

## 依赖验证
本 Skill 依赖的 `equal-data` 包可通过以下方式验证：
- PyPI 页面: https://pypi.org/project/equal-data/
- 源码仓库: https://github.com/kjiujing/equal-data

## 权限说明
- **需要环境变量**: `KJJ_API_TOKEN`（从看究竟官网获取）
- **本地文件写入**: `~/.openclaw/openclaw.json`（用于缓存 Token）
- **网络访问**: 仅限 api.kjiujing.com


