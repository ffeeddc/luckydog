Table of Contents
=================

   * [LUCKY-DOG-API 使用说明](#LUCKY-DOG-API)
      * [<strong>1. 智能合约</strong>](#1-智能合约)
         * [1.1 luckydog.createDog(owner, seniority, name, gene, img, father, mother,trait,male_rest_time,female_rest_time)](#11-luckydog.createDog)
         * [1.2 luckydog.createTrade(dog_id,type,amount)](#12-appsdbgetmodel-cond)
         * [1.3 luckydog.cancelTrade(tid)](#13-luckydog.cancelTrade)
         * [1.4 luckydog.presentDog(dog_id,uid)](#14-luckydog.presentDog)
         * [1.5 luckydog.payDog(tid)](#15-luckydog.payDog)
         * [1.6 luckydog.payMatch(tid,dog_id)](#16-luckydog.payMatch)
      * [2. 查询接口](#2-查询接口)
         * [2.1 /:uid/dogs](#21-/:uid/dogs)
         * [2.2 /:type/trades](#21-/:type/trades)
         * [2.3 /trade/:tid](#21-/trade/:tid)
         * [2.4 /dog/:dog_id](#21-/dog/:dog_id)
      * [3. 调用说明](#2-调用说明)
               * [3.1 测试环境](#21-测试环境)
               * [3.2 正式环境](#21-正式环境)
               
Created by [gh-md-toc](https://github.com/ekalinin/github-markdown-toc)
         
         
# LUCKY-DOG-API 使用说明


## **1. 智能合约**

### 1.1 `1000` luckydog.createDog(owner, seniority, name, gene, img, father, mother,trait,male_rest_time,female_rest_time)

- `owner` 狗主人地址 如：ALoY6zPALAN2YHDvzdipExs6CfH54wKakQ
- `seniority` 狗代数
- `name` 狗名称
- `gene` 狗基因
- `img` 狗头像地址
- `father` 狗爸爸ID
- `mother` 狗妈妈ID
- `trait` 狗特性
- `male_rest_time` 母狗繁育后修养时间
- `female_rest_time` 公狗繁育后修养时间

> 创建狗接口 在测试和初始化是时使用 

### 1.2 `1001` luckydog.createTrade(dog_id,type,amount)

- `dog_id` 要参与交易的狗ID
- `type` 交易类型 0:售卖,1:繁育匹配
- `amount` 交易金额 100000000=1 XAS

> 创建交易 包括售卖和繁育匹配

### 1.3 `1002` luckydog.cancelTrade(tid)

- `tid` 要取消的交易ID

> 取消交易 包括售卖和繁育匹配

### 1.4 `1003` luckydog.presentDog(dog_id,uid)

- `dog_id` 要参与赠送的狗ID
- `uid` 赠送给的用户的地址 如：ALoY6zPALAN2YHDvzdipExs6CfH54wKakQ

> 赠送狗 

### 1.5 `1004` luckydog.payDog(tid)

- `tid` 要支付狗的的交易ID

> 购买狗支付接口 

### 1.6 `1005` luckydog.payMatch(tid,dog_id)

- `tid` 要繁育匹配的交易ID
- `dog_id` 自己要参与繁育的狗ID

> 支付繁育匹配接口 


## **2. 查询接口**

### 2.1 `GET` /:uid/dogs

- `uid` 查询的用户的地址 如：ALoY6zPALAN2YHDvzdipExs6CfH54wKakQ

> 查询用户的所有已生育的狗

返回:

```
{ 
  dogs: mydogs, //狗组数
  count: count  //狗的数量
}
狗的具体结构：
fields: [
    {
      name: 'id',//自增ID
      type: 'String',
      length: 32,
      not_null: true,
      primary_key: true
    },
    {
      name: 'tid',//transID
      type: 'String',
      length: 64,
      not_null: true,
      unique: true,
      index: true
    },
    {
      name: 'owner',//拥有人
      type: 'String',
      length: 50,
      not_null: true,
      index: true
    },
    {
      name: 'seniority',//代数
      type: 'Number',
      not_null: true
    },
    {
      name: 'name',//昵称
      type: 'String',
      length: 50,
      not_null: true
    },
    {
      name: 'gene',//基因编码
      type: 'String',
      length: 50,
      not_null: true
    },
    {
      name: 'img',//图片地址
      type: 'String',
      length: 50,
      not_null: true
    },
    {
      name: 'sex',//性别
      type: 'Number'
    },
    {
      name: 'father',//父亲
      type: 'String',
      length: 50,
      index: true
    },
    {
      name: 'mother',//母亲
      type: 'String',
      length: 50,
      index: true
    },
    {
      name: 'ancestor',//三代信息
      type: 'String',
      length: 500,
      not_null: true
    },
    {
      name: 'trait',//特质
      type: 'String',
      length: 500,
      not_null: true
    },
    {
      name: 'star_sign',//星座
      type: 'String',
      length: 50,
      not_null: true
    },
    {
      name: 'pregnant_time',//怀孕时间
      type: 'String',
      length: 50,
      not_null: true
    },
    {
      name: 'born_time',//出生时间
      type: 'Number',
      not_null: true
    },
    {
      name: 'match_time',//配对次数
      type: 'Number',
      not_null: true,
      default: 0
    },
    {
      name: 'last_match_time',//上次配对时间
      type: 'Number',
      default: 0
    },
    {
      name: 'match_cooling_time',//匹配冷却时间
      type: 'Number',
      default: 0
    },
    {
      name: 'male_rest_time',//公性修整时间
      type: 'Number',
      not_null: true
    },
    {
      name: 'female_rest_time',//母性修整时间
      type: 'Number',
      not_null: true
    },
    {
      name: 'curr_match_price',//当前配对价格
      type: 'String',
      length: 50
    },
    {
      name: 'curr_price',//当前售价
      type: 'String',
      length: 50
    }
]
```

### 2.2 `GET` /:type/trades

- `type`  交易类型 0:售卖,1:繁育匹配
- `query.sortBy` 排序字段
- `query.limit` 每页大小
- `query.offset` 页码 从0开始

> 按类型查询所有交易 
> query参数使用 参见 [Dapp核心开发流程解析-4.3自定义查询接口](https://github.com/AschPlatform/asch/blob/master/docs/dapp_docs/Dapp%E6%A0%B8%E5%BF%83%E5%BC%80%E5%8F%91%E6%B5%81%E7%A8%8B%E8%A7%A3%E6%9E%90.md)

返回:

```
{
  trades: trades //所有交易
}
交易的具体结构：
fields: [
    {
      name: 'id',//自增ID
      type: 'String',
      length: 32,
      not_null: true,
      primary_key: true
    },
    {
      name: 'tid',//transID
      type: 'String',
      length: 64,
      not_null: true,
      unique: true,
      index: true
    },
    {
      name: 'initiator',//发起人
      type: 'String',
      length: 50,
      not_null: true,
      index: true
    },
    {
      name: 'terminator',//终结人
      type: 'String',
      length: 50,
      not_null: true,
      index: true
    },
    {
      name: 'dog_id',//狗ID
      type: 'String',
      length: 50,
      not_null: true
    },
    {
      name: 'dog_born_time',//狗出生时间
      type: 'Number',
      not_null: true,
      index: true
    },
    {
      name: 'type',//类型type(交易/匹配/赠送)
      type: 'Number',
      not_null: true
    },
    {
      name: 'dog_seniority',//代数
      type: 'Number',
      not_null: true
    },
    {
      name: 'dog_img',//图片地址
      type: 'String',
      length: 50,
      not_null: true
    },
    {
      name: 'state',//状态(进行中/交易完成/取消)
      type: 'Number',
      not_null: true,
      index: true
    },
    {
      name: 'amount',//交易金额
      type: 'String',
      length: 50,
      not_null: true,
      index: true
    },
    {
      name: 'create_time',//发起时间
      type: 'Number',
      not_null: true
    }
]
```

### 2.3 `GET` /trade/:tid

- `tid`  交易ID

> 按交易ID查看交易详情

返回:

```
{
  trade: trade //单个交易详情
}
```

### 2.4 `GET` /dog/:dog_id

- `dog_id`  狗ID

> 按交易ID查看交易详情

返回:

```
{
  dog: dog //单个狗详情
}
```

## **3. 调用说明**

### 3.1 测试环境

- `ip`  114.55.75.81
- `端口` 4096
- `应用名称` asch-luckydog-dapp
- `应用ID` f07236d6285b46d7057f6c65d06742f4e7a0b02f2e92ea80769e6a3b3dee05ff

>[测试地址](http://114.55.75.81:4096/dapps/f07236d6285b46d7057f6c65d06742f4e7a0b02f2e92ea80769e6a3b3dee05ff/)

### 3.2 正式环境

// TBD
