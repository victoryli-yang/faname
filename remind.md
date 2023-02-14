<!--
 * @Author: vic-hu
 * @LastEditors: vic-hu
 * @Date: 2020-11-12 16:42:54
 * @LastEditTime: 2023-02-14 11:20:26
 * @Description:
 * @FilePath: /remind.md
-->

# Beancount 说明

### 脚本文件

config.json -- 配置文件项
file.json -- csv路径和导出路径项
priceConfig.json -- 股票基金配置项
main.js -- 批量处理 csv 的脚本
price.js -- 获取股票基金 t+1 日价格，并生成 price 文件(注：持续写入

### bean 文件

main.bean -- 主文件 定义所有账本和账户
accounts.bean -- 账户文件 定义账户
price.bean -- 价格列表(根据脚本自动生成)
files 2020-bean -- 年度账本目录

- 2020-bean -- 年度目录
  - 2020.bean -- 年度总账本
  - 2020-xx.bean -- 月度信用卡账本
  - 2020-cash.bean -- 年度手工输入账本
  - 2020-income.bean -- 年度收入账本
  - 2020-investment.bean -- 年度投资账本
  - 2020-price.bean -- 年度货币账本

### 运行方式

node 环境下

node main.js // 批量生成
node price.js // 获取价格

ps: 需要提前配置好 file.json 的路径和 config.json 的脚本

### 可视化

beancount 是个 Python 项目，安装好 python 后，执行：
pip install beancount
pip install fava
pip install -U fava  // 升级 fava

// 运行 web
fava main.bean

### 自动化处理(不完善)

流程思路
1.通过信用卡账单归集数据
  - ceb 电子邮件 -> pdf 导出
  - cmb 电子对账单下载
2.Excalibur 处理 pdf -> 导出 csv 文件
3.node 脚本批量处理 csv -> 导出 bean 文件

问题
1. Excalibur 处理 pdf 表格文件识别准确率不够高依旧需要人工干预
2. 导出 对帐单流程 比较麻烦
3. 无法对多种账单处理，需要修改代码，最好处理成可配制化

### Excalibur 简介

Excalibur 是一个 pdf 表格识别工具 依赖 camelot
所以需要安装 camelot 在安装 ghostscript
前者需要 python 后者需要 brew

```bash
  excalibur webserver #启动命令
```

Excalibur 本地版本已经被魔改过，操作项目都不需要操作，
下载页面点下载会跳转，此时表明文件已经被保存到本地目录下（303文件夹）

### bql 示例

```sql
  SELECT * FROM 'Liabilities:CreditCard:CEB'
  where (year = 2022 and month = 8 and day >10)
  or (year = 2022 and month = 9 and day <10)
  and number(convert(units(position), 'CNY')) > 0
  and flag = '*'
  -- 查询 2022-08-10 到 2022-09-10 之间的 cny > 0 的消费
```
