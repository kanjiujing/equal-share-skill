---
name: equal-data-skill
description: 看究竟金融数据服务 Skill - 提供 A 股行情、基金、财报、高管增减持、机构动向、龙虎榜、基金画像等专业金融数据查询
author: 看究竟
pypi_package: equal-data
install_required: true
install_command: pip install equal-data==0.0.5
required_env_vars:
  - KJJ_API_TOKEN
---

# equal-data-skill

## 概述

**equal-data-skill** 是基于 PyPI 包 `equal-data` 封装的看究竟(Kanjiujing)金融数据服务 Skill，主要是用于查询A股股票的各个维度统计信息。该模块通过标准化API方式统一了数据资产的对外服务方式，以帮助有需要的技术用户更实时、简洁、轻量的使用相关数据。

## 快速上手

- 安装python运行环境(推荐python3.6+)，并安装equal-data依赖包。

```bash
python -m venv test_env
source test_env/bin/activate
pip install equal-data -i https://pypi.tuna.tsinghua.edu.cn/simple
```

- 根据接口文档，使用python代码获取数据。（如**高管增减持金额排行榜**接口）

```python
from equal_data import KjjApi
import os

# 读取环境变量中的token, 或者读取本地记录的token
token = os.getenv('KJJ_API_TOKEN')

api = KjjApi(token)

# 高管持股变动-增减持金额排行榜列表
data = api.query_kjj_data(
    interfaceId="DRAGON_TIGER_MANAGER_HOLDING_RANK_322EC0A8",
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
| `interfaceId`  | `str`  | 是   | `DRAGON_TIGER_MANAGER_HOLDING_RANK_322EC0A8`     | 接口ID                                                       |
| `period`       | `int` | 否   | `1`      | 1-近1月、2-近3月、3-近半年、4-近1年                          |
| `changeType`   | `int` | 否   | -        | 变动类型（增持：1，减持：-1）                                |
| `pageIndex`    | `int` | 是   | `0`      | 当前页从0开始                                                |
| `pageSize`     | `int` | 是   | `10`     | 每页显示记录数                                               |
| `selfSelected` | `bool` | 否   | `false`  | true: 只看自选 false：全部（默认）                           |
| `sortDesc`     | `str`  | 否   | `1-DESC` | 排序描述 1-ASC/1-DESC 等，1表示增持金额 2增持数量 3占总股本比 4占流通股本比 <br>5净增持股数 6增持均价 |

- 返回格式：json

## 认证方式

本 Skill 需要看究竟 API Token (`KJJ_API_TOKEN`)，支持以下两种方式配置：

看究竟官网注册，获取token，

**方式 B：配置环境变量**。

```bash
export KJJ_API_TOKEN="your_key_here"
```

**方式 C：OpenClaw配置文件:**
在 `~/.openclaw/openclaw.json` 中配置：
```json
{
  "skills": {
    "entries": {
      "equal-data-skill": {
        "enabled": true,
        "env": {
          "KJJ_API_TOKEN": "your_actual_token_here"
        }
      }
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


| 接口ID | 接口名称 | 接口描述 | 分类 | 文档路径 |
|:---:|:---|:---|:---|:---|
| DRAGON_TIGER_WIN_RATE_RANK_1AFFA65 | 龙虎榜-胜率排行榜近1月 | 获取龙虎榜游资胜率排行榜 | 究竟特色数据 | [龙虎榜-胜率排行榜近1月.md](<reference/究竟特色数据/龙虎榜-胜率排行榜近1月.md>) |
| DRAGON_TIGER_STOCK_TRADEDATE_RANK_668D1998 | 龙虎榜单-个股榜 | 获取指定交易日的龙虎榜个股榜单 | 究竟特色数据 | [龙虎榜单-个股榜.md](<reference/究竟特色数据/龙虎榜单-个股榜.md>) |
| DRAGON_TIGER_HOT_MONEY_TRADEDATE_RANK_CBDEEFE9 | 龙虎榜-游资榜 | 获取指定交易日的龙虎榜游资榜单 | 究竟特色数据 | [龙虎榜-游资榜.md](<reference/究竟特色数据/龙虎榜-游资榜.md>) |
| DRAGON_TIGER_DEPT_TRADEDATE_RANK_5F3249C0 | 龙虎榜-营业部榜 | 获取指定交易日的龙虎榜营业部榜单 | 究竟特色数据 | [龙虎榜-营业部榜.md](<reference/究竟特色数据/龙虎榜-营业部榜.md>) |
| DRAGON_TIGER_MARKET_HIGH_TRADEDATE_RANK_55B4FB4 | 龙虎榜-市场高度 | 获取指定交易日的市场高度榜（几天几板） | 究竟特色数据 | [龙虎榜-市场高度.md](<reference/究竟特色数据/龙虎榜-市场高度.md>) |
| DRAGON_TIGER_MANAGER_HOLDING_RANK_322EC0A8 | 高管持股-增减持金额排行榜 | 获取高管持股-增减持金额排行榜 | 究竟特色数据 | [高管持股-增减持金额排行榜.md](<reference/究竟特色数据/高管持股-增减持金额排行榜.md>) |
| DRAGON_TIGER_MANAGER_HOLDING_CHANGE_LIST_E8127FAB | 高管持股-增减持变动明细列表 | 获取高管持股-增减持变动明细列表 | 究竟特色数据 | [高管持股-增减持变动明细列表.md](<reference/究竟特色数据/高管持股-增减持变动明细列表.md>) |
| DRAGON_TIGER_MANAGER_HOLDING_PLAN_LIST_1AF0B10B | 高管增减持计划列表 | 获取高管增减持计划列表 | 究竟特色数据 | [高管增减持计划列表.md](<reference/究竟特色数据/高管增减持计划列表.md>) |
| DRAGON_TIGER_MANAGER_HOLDING_STOCKCODE_OPT_DETAIL_D294B48C | 高管增减持操作明细 | 获取高管增减持操作明细 | 究竟特色数据 | [高管增减持操作明细.md](<reference/究竟特色数据/高管增减持操作明细.md>) |
| DRAGON_TIGER_MANAGER_HOLDING_STOCKCODE_PLAN_DETAIL_B5554323 | 高管单条增减持计划详情 | 获取高管单条增减持计划详情数据 | 究竟特色数据 | [高管单条增减持计划详情.md](<reference/究竟特色数据/高管单条增减持计划详情.md>) |
| DRAGON_TIGER_MANAGER_HOLDING_STOCKCODE_BASIC_INFO_937D50E | 高管持股数据分析 | 高管持股数据分析 | 究竟特色数据 | [高管持股数据分析.md](<reference/究竟特色数据/高管持股数据分析.md>) |
| DRAGON_TIGER_AGENCY_PAGE_LIST_V250_97962782 | 机构动向列表数据 | 机构动向列表数据 | 究竟特色数据 | [机构动向列表数据.md](<reference/究竟特色数据/机构动向列表数据.md>) |
| DRAGON_TIGER_AGENCY_BASIC_INFO_V250_829F10F3 | 机构风云榜榜单列表 | 机构风云榜榜单列表 | 究竟特色数据 | [机构风云榜榜单列表.md](<reference/究竟特色数据/机构风云榜榜单列表.md>) |
| DRAGON_TIGER_AGENCY_RANK_LIST_V250_B927F2B8 | 机构风云榜榜单详情数据 | 机构风云榜榜单详情数据 | 究竟特色数据 | [机构风云榜榜单详情数据.md](<reference/究竟特色数据/机构风云榜榜单详情数据.md>) |
| DRAGON_TIGER_AGENCY_HOLDER_STOCK_LIST_986A9741 | 机构持仓列表 | 机构持仓列表 | 究竟特色数据 | [机构持仓列表.md](<reference/究竟特色数据/机构持仓列表.md>) |
| DRAGON_TIGER_AGENCY_DETAIL_400A302A | 机构详情 | 机构详情 | 究竟特色数据 | [机构详情.md](<reference/究竟特色数据/机构详情.md>) |
| DRAGON_TIGER_AGENCY_CURRENT_LIST_9D50A506 | 机构本期持股列表 | 机构本期持股列表 | 究竟特色数据 | [机构本期持股列表.md](<reference/究竟特色数据/机构本期持股列表.md>) |
| DRAGON_TIGER_FREE_BATCH_LIST_FB76F3D6 | 限售解禁数据列表（历史解禁/预告/仅自选） | 限售解禁数据列表（历史解禁/预告/仅自选） | 究竟特色数据 | [限售解禁数据列表（历史解禁_预告_仅自选）.md](<reference/究竟特色数据/限售解禁数据列表（历史解禁_预告_仅自选）.md>) |
| DRAGON_TIGER_FREE_BATCH_STOCKCODE_DETAIL_1CA5561F | 限售解禁详情页 | 限售解禁详情页 | 究竟特色数据 | [限售解禁详情页.md](<reference/究竟特色数据/限售解禁详情页.md>) |
| DRAGON_TIGER_FREE_BATCH_STOCKCODE_ANALYSIS_D5B7BAB8 | 限售解禁数据分析接口 | 限售解禁数据分析接口 | 究竟特色数据 | [限售解禁数据分析接口.md](<reference/究竟特色数据/限售解禁数据分析接口.md>) |
| DRAGON_TIGER_BULK_DATA_ACTIVE_DEPT_LIST_37C4AE61 | 大宗数据-活跃营业部 | 大宗数据-活跃营业部 | 究竟特色数据 | [大宗数据-活跃营业部.md](<reference/究竟特色数据/大宗数据-活跃营业部.md>) |
| DRAGON_TIGER_BULK_DATA_ACTIVE_STOCK_LIST_2477A81C | 大宗数据-活跃个股 | 大宗数据-活跃个股 | 究竟特色数据 | [大宗数据-活跃个股.md](<reference/究竟特色数据/大宗数据-活跃个股.md>) |
| DRAGON_TIGER_PERFORMANCE_THUNDERSTORM_A138D59 | 业绩预告-业绩暴雷、业绩预增 | 业绩预告-业绩暴雷、业绩预增 | 究竟特色数据 | [业绩预告-业绩暴雷、业绩预增.md](<reference/究竟特色数据/业绩预告-业绩暴雷、业绩预增.md>) |
| DRAGON_TIGER_BIG_CONTRACT_LIST_3C04CC28 | 重大合同-数据列表 | 重大合同-数据列表 | 究竟特色数据 | [重大合同-数据列表.md](<reference/究竟特色数据/重大合同-数据列表.md>) |
| DRAGON_TIGER_BONUS_LIST_CE25AB7E | 分红送转-预案/实施 | 分红送转-预案/实施 | 究竟特色数据 | [分红送转-预案_实施.md](<reference/究竟特色数据/分红送转-预案_实施.md>) |
| DRAGON_TIGER_AGENCY_RESEARCH_LIST_BD40F7FC | 机构调研列表 | 机构调研列表 | 究竟特色数据 | [机构调研列表.md](<reference/究竟特色数据/机构调研列表.md>) |
| LISTEDCOMPANY_MANAGER_LIST_FF45CB43 | 上市公司管理层信息 | 上市公司管理层信息：按股票代码/名称（可多选）、排名日期、排名等条件动态筛选，<br>整体分页返回上市公司管理层信息。 | 股票基础数据 | [上市公司管理层信息.md](<reference/股票基础数据/上市公司管理层信息.md>) |
| LISTEDCOMPANY_TEN_SHAREHOLDER_LIST_75B38FFF | 十大股东/十大流通股东 | 十大股东/十大流通股东：按股票代码/名称（可多选）、数据日期、股东类型等条件动态筛选，<br>整体分页返回上市公司十大股东、十大流通股东数据。 | 股票基础数据 | [十大股东_十大流通股东.md](<reference/股票基础数据/十大股东_十大流通股东.md>) |
| LISTEDCOMPANY_HOLDER_NUM_6ED90164 | 股东人数列表数据 | 股东人数列表数据：股票代码动态筛选，返回上市公司股东人数列表数据。 | 股票基础数据 | [股东人数列表数据.md](<reference/股票基础数据/股东人数列表数据.md>) |
| LISTEDCOMPANY_INSTITUTION_HOLDING_DETAIL_DBC4812E | 公司详情页-股东股本 -机构持仓明细 | 公司详情页-股东股本 -机构持仓明细 | 股票基础数据 | [公司详情页-股东股本_-机构持仓明细.md](<reference/股票基础数据/公司详情页-股东股本_-机构持仓明细.md>) |
| LISTEDCOMPANY_LATEST_FINANCE_INDEX_4A98062C | 公司详情页-最新一期指标展示 | 公司详情页-最新一期指标展示 | 股票基础数据 | [公司详情页-最新一期指标展示.md](<reference/股票基础数据/公司详情页-最新一期指标展示.md>) |
| STOCK_LIST_976A0399 | 基本股票列表/公司信息 | 基本股票列表/公司信息：按股票代码/名称（可多选）、上市日期、退市日期、交易所、<br>证券类别等条件动态筛选，整体分页返回上市公司基础信息。 | 股票基础数据 | [基本股票列表_公司信息.md](<reference/股票基础数据/基本股票列表_公司信息.md>) |
| STOCK_TRADE_DATE_LIST_A691BBFA | 交易日期列表 | 获取交易日期列表 | 股票基础数据 | [交易日期列表.md](<reference/股票基础数据/交易日期列表.md>) |
| STOCK_CHANGE_NAME_LIST_6C169374 | 股票更名列表 | 获取股票更名列表 | 股票基础数据 | [股票更名列表.md](<reference/股票基础数据/股票更名列表.md>) |
| STOCK_ST_LIST_D9254E18 | ST股票列表 | 获取ST股票列表 | 股票基础数据 | [ST股票列表.md](<reference/股票基础数据/ST股票列表.md>) |
| STOCK_HOT_INDUSTRY_STOCK_LIST_690C1159 | 热门行业板块-股票列表 | 获取热门行业板块-股票列表 | 股票基础数据 | [热门行业板块-股票列表.md](<reference/股票基础数据/热门行业板块-股票列表.md>) |
| STOCK_HOT_THEME_STOCK_LIST_21FB8583 | 热门概念板块-股票列表 | 获取热门概念板块-股票列表 | 股票基础数据 | [热门概念板块-股票列表.md](<reference/股票基础数据/热门概念板块-股票列表.md>) |
| FINANCE_INDEX_MAJOR_INDICATORS_BDA2853F | 主要财务指标 | 主要财务指标 | 财务数据 | [主要财务指标.md](<reference/财务数据/主要财务指标.md>) |
| FINANCE_INDEX_BUSINESS_ANALYSIS_HISTORY_DATA_A113AD31 | 主营业务数据分析历史数据 | 主营业务数据分析历史数据 | 财务数据 | [主营业务数据分析历史数据.md](<reference/财务数据/主营业务数据分析历史数据.md>) |
| NEWS_INFO_NEWS_LIST_530922EB | 快讯信息（近一个月的快讯） | 快讯信息（近一个月的快讯） | 资讯信息 | [快讯信息（近一个月的快讯）.md](<reference/资讯信息/快讯信息（近一个月的快讯）.md>) |
| NEWS_INFO_ARTICLE_LIST_D6DA008D | 文章信息 | 文章信息 | 资讯信息 | [文章信息.md](<reference/资讯信息/文章信息.md>) |
| NEWS_INFO_NOTICE_ANNOUNCEMENT_LIST_53A04ED2 | 公告信息 | 公告信息 | 资讯信息 | [公告信息.md](<reference/资讯信息/公告信息.md>) |
| STOCK_QUOTE_REAL_TIME_QUOTE_LIST_3E577EB | 实时行情列表 | 获取实时行情列表 | 股票行情数据 | [实时行情列表.md](<reference/股票行情数据/实时行情列表.md>) |
| STOCK_QUOTE_HISTORY_QUOTE_LIST_C82F9954 | 历史日K行情数据 | 历史日K行情数据 | 股票行情数据 | [历史日K行情数据.md](<reference/股票行情数据/历史日K行情数据.md>) |
| DRAGON_TIGER_DATE_LIST_B10D430C | 龙虎榜日期列表 | 获取龙虎榜可用的历史交易日期列表 | 打板专题数据 | [龙虎榜日期列表.md](<reference/打板专题数据/龙虎榜日期列表.md>) |
| DRAGON_TIGER_DEPT_BELONG_HOT_MONEY_8CF53BF9 | 龙虎榜机构（营业部）-所属游资席位 | 根据营业部全称查询所属游资席位列表 | 打板专题数据 | [龙虎榜机构（营业部）-所属游资席位.md](<reference/打板专题数据/龙虎榜机构（营业部）-所属游资席位.md>) |
| DRAGON_TIGER_DEPT_HOLDING_DETIAL_LIST_F4578FA0 | 龙虎榜机构（营业部）-操作明细 | 查询指定营业部的历史操作明细 | 打板专题数据 | [龙虎榜机构（营业部）-操作明细.md](<reference/打板专题数据/龙虎榜机构（营业部）-操作明细.md>) |
| DRAGON_TIGER_DETAIL_HOTMONEY_ANALYSIS_FBB71945 | 龙虎榜-游资特色指标分析（近1年/近1月） | 获取指定游资的交易分析数据 | 打板专题数据 | [龙虎榜-游资特色指标分析（近1年_近1月）.md](<reference/打板专题数据/龙虎榜-游资特色指标分析（近1年_近1月）.md>) |
| DRAGON_TIGER_HOT_MONEY_DTL249_B4962607 | 游资基本信息 | 查询游资详情，返回游资信息及相关营业部信息 | 打板专题数据 | [游资基本信息.md](<reference/打板专题数据/游资基本信息.md>) |
| DRAGON_TIGER_HOT_MONEY_OPT_BF4B9B9B | 游资每日操作明细 | 查询游资在指定交易日附近的近期操作明细 | 打板专题数据 | [游资每日操作明细.md](<reference/打板专题数据/游资每日操作明细.md>) |

## 分类统计

| 分类 | 接口数量 |
|:---|:---|
| 究竟特色数据 | 26 |
| 股票基础数据 | 11 |
| 财务数据 | 2 |
| 资讯信息 | 3 |
| 股票行情数据 | 2 |
| 打板专题数据 | 6 |
| **合计** | **50** |

## 数据来源与依赖
- **官方文档**: `http://equal-data.com/docs`
- **PYPI包地址**: `https://pypi.org/project/equal-data/`
- **官网**: `[https://equal-data.com/](https://equal-data.com/)`
- **数据用途**: 仅用于获取行情数据，不涉及交易操作
- **开源依赖**:
  - requests (Apache 2.0)
  - pandas (BSD 3-Clause)
  - equal-data

## 依赖验证
本 Skill 依赖的 `equal-data` 包可通过以下方式验证：
- PyPI 页面: https://pypi.org/project/equal-data/
- 源码仓库: https://github.com/kanjiujing/equal-share-skill/

## 权限说明
- **需要环境变量**: `KJJ_API_TOKEN`（从看究竟官网获取）
- **本地文件写入**: `~/.openclaw/openclaw.json`（用于缓存 Token）


