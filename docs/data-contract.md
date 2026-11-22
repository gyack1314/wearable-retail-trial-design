# 业务资料契约

所有人物、家庭、设备、供应商和交易均为本地合成资料。金额使用整数分，时长字段的单位写在列说明中。时间戳含时区，起止区间均为左闭右开。空值表示未观察或未提供，数值零保留其真实含义。

prob_pair 是来源时段形成时的分配机会，不是通过成交后拟合出的概率。退款关联原 order。future_blocks 为下一轮候选营业时段，尚未形成项目安排。S1/S2 共用 K1，S3/S4 共用 K2，移动和消毒占用套件。

## people.csv

人员主档。第一列是物理记录的唯一键。

- `person` 表示人员编号，类型为 str。
- `household` 表示登记家庭编号，类型为 str。
- `segment` 表示长期客群，类型为 str。
- `home_zone` 表示常居时区，类型为 str。
## blocks.csv

原定轮换时段和真实分配机会。第一列是物理记录的唯一键。

- `block` 表示时段，类型为 str。
- `store` 表示门店，类型为 str。
- `start` 表示开始，类型为 datetime。
- `end` 表示结束，类型为 datetime。
- `assigned` 表示分配路径，类型为 str。
- `prob_pair` 表示该时段分到组合路径的机会，类型为 float。
- `announced` 表示是否公告专场，类型为 int。
## visits.csv

跨门店顾客到访和实际接触。第一列是物理记录的唯一键。

- `visit` 表示到访，类型为 str。
- `person` 表示顾客，类型为 str。
- `block` 表示原定时段，类型为 str。
- `actual_path` 表示实际路径，类型为 str。
- `reason` 表示偏离原因，类型为 str。
- `at` 表示到访时间，类型为 datetime。
## orders.csv

离店后成交及撤单事实。第一列是物理记录的唯一键。

- `record` 表示记录，类型为 str。
- `order` 表示订单身份，类型为 str。
- `person` 表示顾客，类型为 str。
- `at` 表示发生时间，类型为 datetime。
- `kind` 表示支付或退款，类型为 str。
- `cents` 表示正数金额，类型为 int。
- `channel` 表示成交渠道，类型为 str。
## kits.csv

演示套件及可使用门店。第一列是物理记录的唯一键。

- `kit` 表示套件，类型为 str。
- `stores` 表示可服务门店集合，类型为 str。
- `service` 表示支持的路径，类型为 str。
- `available_start` 表示可用开始，类型为 datetime。
- `available_end` 表示可用结束，类型为 datetime。
## future_blocks.csv

下一轮营业与专场约束。第一列是物理记录的唯一键。

- `block` 表示候选时段，类型为 str。
- `store` 表示门店，类型为 str。
- `start` 表示开始，类型为 datetime。
- `end` 表示结束，类型为 datetime。
- `staff` 表示可用人员数，类型为 int。
- `fixed_path` 表示已公告路径，类型为 str，允许空值。
## outages.csv

设备故障事实。第一列是物理记录的唯一键。

- `outage` 表示故障，类型为 str。
- `kit` 表示套件，类型为 str。
- `start` 表示故障开始，类型为 datetime。
- `end` 表示故障结束，类型为 datetime。
- `reported` 表示报告，类型为 datetime。

数值条款、可调整范围及业务枚举见 data/terms.json。数据契约定义来源记录和已存在的协议，分析方法及内部实现由项目使用者按业务需求选择。
