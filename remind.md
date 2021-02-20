<!--
 * @Author: vic-hu
 * @LastEditors: vic-hu
 * @Date: 2020-11-12 16:42:54
 * @LastEditTime: 2021-02-19 16:16:12
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
