# AMD EPYC VPS 推荐：分清 7003/9004/9005 代际差异，按线路挑对套餐不花冤枉钱

搜“AMD EPYC VPS 推荐”的人，多半已经跨过了第一道坎——知道要买 EPYC，而不是随便找个便宜 VPS。真正卡住的地方在后面：同样写着“AMD EPYC”，有的套餐一年三十几美元，有的一个月两百多美元，配置看起来还差不多。这中间的钱到底花在哪了，值不值，才是决定你下单还是关掉页面的关键。

这篇文章按这个顺序讲：EPYC 到底有几代、便宜和贵差在哪、DMIT 的三个硬件平台和三条线路分别对应什么需求，最后把洛杉矶、香港、东京的在售档位摊开对比，让你对着自己的用途直接挑。

## EPYC 是四代同堂的产品线，不是一款 CPU

AMD EPYC 2017 年上线，至今已经迭代到第六代。现在 VPS 市场上同时在架销售的，主要集中在这四代：

- **7002（Rome，Zen 2）**：2019 年的平台，7K62、7532、7642 这类编号基本都是那一代云厂商定制型号
- **7003（Milan，Zen 3）**：2021 年，低价套餐的绝对主力，7B13、7443P、7763 都属这一代
- **9004（Genoa，Zen 4）**：单核和内存带宽明显上一台阶，AVX-512 从这里开始支持
- **9005（Turin，Zen 5）**：目前最新的一代在售平台，配 DDR5 ECC

从 Rome 的 Zen 2 到 Turin 的 Zen 5，中间隔了三次架构更替。同样是“2 核 EPYC”，跑编译、数据库、Node 后端这类吃单核的场景，体验差距是按代算的，不是按百分比算的。

判断方法很简单：**推广文案只写“AMD EPYC 处理器”而不写代际的，默认按老平台理解。**真正用新平台的商家一定会把型号标出来，因为那是卖点。DMIT 的做法是把平台代号直接写进套餐名，AS3 对应 EPYC 7003、AN4 对应 9004、AN5 对应 9005，看名字就知道自己买的是哪一代。

## 便宜的那批 EPYC VPS，便宜在哪

搞清楚成本结构，就不容易被“EPYC 只要 38 元/月”这类话术带偏。省下来的钱主要来自三个地方。

**核数不是你的核数。** 低价档几乎都是共享 vCPU，物理机几十个核心切碎卖给一屋子邻居，邻居跑满，你那“2 核”跟着抖。没写“独享核心”的，一律按共享理解。

**内存成本。** 这一轮 DDR5 涨价幅度很大，新平台套餐的硬件成本被直接推高，这也是新一代平台比老平台贵的现实原因之一，跟商家想不想让利关系不大。

**线路。** 这是最容易被忽略、又最影响实际体验的一项。跨境回程路由的成本远高于多切一个核心给你的成本。对国内访问为主的用途，CN2 GIA、9929、CMIN2 这些优化线路的价值，通常高于套餐里多出来的那一个核。

所以选 EPYC VPS 的正确顺序，不是“先看核数”，而是**先定线路，再定平台，最后才在档位里挑配置**。

## DMIT 的平台划分：AS3 / AN4 / AN5

DMIT 是 2017 年开始做 VPS 业务的美国注册公司，机房覆盖洛杉矶、香港、东京，产品以 KVM 虚拟化的 VPS 和裸金属为主，支持支付宝、微信支付、PayPal 和信用卡，有中文工单。真正影响选择的，是它的两层划分。

第一层是硬件平台，也就是 CPU 代际：

- **AS3** —— AMD EPYC 7003 系列
- **AN4** —— AMD EPYC 9004 系列
- **AN5** —— AMD EPYC 9005 系列

第二层是网络线路，分成 Premium（Pro）、Eyeball（EB）、Tier 1（T1）三条。这两层是正交的，同一个平台可以选不同线路，同一线路也有不同平台的版本。

有一点得提前说清楚：DMIT 官方对 AS3 平台有过明确提示——该平台仍处于持续优化阶段，磁盘性能和 SLA 可能低于成熟平台。这话不是营销修辞，介意这一点的，买之前先做测试再部署重要业务。（另外，官方把香港 Eyeball 网络标注为 Beta，产品和路由仍在调整，官方也不建议直接用于对稳定性要求很高的生产环境。）

## 三条线路，分别适合谁

**Premium（Pro）** 是最高一档。洛杉矶 Premium 的典型路由是电信去程 CN2 GIA（AS4809），联通去程直连 AS4837，移动去程走香港移动 AS58453，三网回程统一走 CN2 GIA。香港 Premium 对应的是 CN2 GIA（AS23764）。这一档的定位很清楚：晚高峰不掉链子、延迟低、丢包少，代价是单价最高。

**Eyeball（EB）** 是中间档。电信走 AS9929 与 AS58807 负载均衡，联通主要走 AS9929，移动主要走 AS58807（CMIN2）。移动用户在这条线上拿到的体验接近 Premium，价格低一截，而且同档位给到的流量通常比 Premium 更大。适合移动/联通为主、或者预算有限但想要大陆访问体验的场景。

**Tier 1（T1）** 是国际线路，纯国际 BGP，不做中国方向优化。国内直连体验一般，胜在带宽大、流量多、价格低——$36.90/年 的 WEE 就是这条线上的常青款。做落地、中转、给海外访问兜底，选这条最划算。

记住一句话就行：**电信党优先 Premium，移动党优先 Eyeball，图便宜做中转上 Tier 1。**

## 洛杉矶全档位对比（AS3 平台，EPYC 7003）

以下为 DMIT 洛杉矶 AS3 平台目前在售的三条线路档位。所有档位均为 KVM 虚拟化、1 IPv4 + 1 IPv6 /64、流量双向计费、高速流量用完后降速不限流（不停机），支持月付、季付、半年付、年付。

### Premium（Pro）—— 三网回程 CN2 GIA

| 套餐 | CPU / 内存 / SSD | 流量 @ 带宽 | 超量后 | 价格 | 购买 |
| --- | --- | --- | --- | --- | --- |
| LAX.AS3.Pro.TINY | 1 核 / 2GB / 20GB | 1000GB @ 1Gbps | 4Mbps 不限流 | $10.90/月 | [前往 DMIT 订单页查看](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.Pro.Pocket | 2 核 / 2GB / 40GB | 1500GB @ 4Gbps | 4Mbps 不限流 | $16.90/月 | [前往 DMIT 订单页查看](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.Pro.STARTER | 2 核 / 2GB / 80GB | 3000GB @ 10Gbps | 4Mbps 不限流 | $34.90/月 | [前往 DMIT 订单页查看](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.Pro.MINI | 4 核 / 4GB / 80GB | 5000GB @ 10Gbps | 8Mbps 不限流 | $62.90/月 | [前往 DMIT 订单页查看](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.Pro.MICRO | 4 核 / 4GB / 160GB | 7000GB @ 10Gbps | 8Mbps 不限流 | $87.90/月 | [前往 DMIT 订单页查看](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.Pro.MEDIUM | 6 核 / 8GB / 160GB | 14000GB @ 10Gbps | 10Mbps 不限流 | $199.90/月 | [前往 DMIT 订单页查看](https://www.dmit.io/aff.php?aff=12046) |

### Eyeball（EB）—— 9929 + CMIN2

| 套餐 | CPU / 内存 / SSD | 流量 @ 带宽 | 超量后 | 价格 | 购买 |
| --- | --- | --- | --- | --- | --- |
| LAX.AS3.EB.TINY | 1 核 / 2GB / 20GB | 1500GB @ 2Gbps | 4Mbps 不限流 | $10.90/月 | [查看 Eyeball 档位](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.EB.Pocket | 2 核 / 2GB / 40GB | 3000GB @ 4Gbps | 4Mbps 不限流 | $16.90/月 | [查看 Eyeball 档位](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.EB.STARTER | 2 核 / 2GB / 80GB | 5000GB @ 10Gbps | 4Mbps 不限流 | $34.90/月 | [查看 Eyeball 档位](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.EB.MINI | 4 核 / 4GB / 80GB | 10000GB @ 10Gbps | 8Mbps 不限流 | $62.90/月 | [查看 Eyeball 档位](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.EB.MICRO | 4 核 / 4GB / 160GB | 14000GB @ 10Gbps | 8Mbps 不限流 | $87.90/月 | [查看 Eyeball 档位](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.EB.MEDIUM | 6 核 / 8GB / 160GB | 30000GB @ 10Gbps | 10Mbps 不限流 | $199.90/月 | [查看 Eyeball 档位](https://www.dmit.io/aff.php?aff=12046) |

同样价位下，Eyeball 的流量基本是 Premium 的两倍左右。TINY 这一档差距没那么大（1500GB 对 1000GB），档位越高差距越明显。

### Tier 1（T1）—— 国际 BGP

| 套餐 | CPU / 内存 / SSD | 流量 @ 带宽 | 超量后 | 价格 | 购买 |
| --- | --- | --- | --- | --- | --- |
| LAX.AS3.T1.WEE | 1 核 / 1GB / 20GB | 1000GB @ 4Gbps | 100Mbps 不限流 | $36.90/年 | [查看 Tier 1 档位](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.T1.TINY | 1 核 / 1GB / 20GB | 2000GB @ 4Gbps | 200Mbps 不限流 | $6.90/月 | [查看 Tier 1 档位](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.T1.STARTER | 2 核 / 2GB / 40GB | 4000GB @ 10Gbps | 200Mbps 不限流 | $12.90/月 | [查看 Tier 1 档位](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.T1.MINI | 2 核 / 4GB / 80GB | 8000GB @ 10Gbps | 200Mbps 不限流 | $21.90/月 | [查看 Tier 1 档位](https://www.dmit.io/aff.php?aff=12046) |
| LAX.AS3.T1.MICRO | 4 核 / 4GB / 120GB | 16000GB @ 10Gbps | 500Mbps 不限流 | $32.90/月 | [查看 Tier 1 档位](https://www.dmit.io/aff.php?aff=12046) |

Tier 1 超量后的降速档比 Premium/Eyeball 高得多（100–500Mbps vs 4–10Mbps），这也是它适合做大流量中转的原因之一。

## AN5 / AN4 平台：新一代贵在哪

AN5（EPYC 9005 + DDR5）的洛杉矶 Premium 档位，配置梯度跟 AS3 不完全一样，价格整体高一档：

| 套餐 | CPU / 内存 / SSD | 流量 @ 带宽 | 价格 | 购买 |
| --- | --- | --- | --- | --- |
| LAX.AN5.Pro.TINY | 1 核 / 2GB / 20GB | 1000GB @ 1Gbps | $12.98/月（部分周期 $37.99/季） | [查看 AN5 Premium 档位](https://www.dmit.io/cart.php?region=los-angeles&generation=an5&network=premium&aff=12046) |
| LAX.AN5.Pro.Pocket | 1 核 / 2GB / 40GB | 1500GB @ 4Gbps | $18.90/月（部分周期 $56.70/季） | [查看 AN5 Premium 档位](https://www.dmit.io/cart.php?region=los-angeles&generation=an5&network=premium&aff=12046) |
| LAX.AN5.Pro.STARTER | 2 核 / 2GB / 80GB | 3000GB @ 10Gbps | $38.90/月 | [查看 AN5 Premium 档位](https://www.dmit.io/cart.php?region=los-angeles&generation=an5&network=premium&aff=12046) |
| LAX.AN5.Pro.MINI | 2 核 / 4GB / 80GB | 5000GB @ 10Gbps | $76.90/月 | [查看 AN5 Premium 档位](https://www.dmit.io/cart.php?region=los-angeles&generation=an5&network=premium&aff=12046) |
| LAX.AN5.Pro.MICRO | 4 核 / 4GB / 160GB | 7000GB @ 10Gbps | $99.90/月 | [查看 AN5 Premium 档位](https://www.dmit.io/cart.php?region=los-angeles&generation=an5&network=premium&aff=12046) |
| LAX.AN5.Pro.MEDIUM | 4 核 / 8GB / 160GB | 14000GB @ 10Gbps | $219.90/月 | [查看 AN5 Premium 档位](https://www.dmit.io/cart.php?region=los-angeles&generation=an5&network=premium&aff=12046) |

Eyeball 侧的 AN5 有更高档位可选，包括 4 核 4GB / 80GB 配 10TB 流量、4 核 4GB / 160GB 配 14TB、6 核 8GB / 160GB 配 30TB，以及 8 核 16GB、12 核 24GB 的大规格机型。

**关于 AN5，有件事必须提醒：这个系列经历过下架和返场，同一档位在不同时期出现过不同的报价和计费周期（例如返场后部分季付选项被取消，低配档一度取消月付）。**如果你看到的价格和本文表格不一致，以订单页实时显示为准，这不是谁写错了，是它真的在变。

洛杉矶 Tier 1 侧，AN5 分成了 VOLUME 和 GENERAL 两个系列——VOLUME 给更多流量，GENERAL 给更高的内存/硬盘规格：

| 套餐 | CPU / 内存 / SSD | 流量 @ 带宽 | 价格 | 购买 |
| --- | --- | --- | --- | --- |
| AN5.T1.V2C2G（VOLUME） | 2 核 / 2GB / 40GB | 5000GB @ 10Gbps | $14.90/月 | [查看 AN5 Tier 1 档位](https://www.dmit.io/cart.php?region=los-angeles&generation=an5&network=tier-1&aff=12046) |
| AN5.T1.V2C4G（VOLUME） | 2 核 / 4GB / 80GB | 10000GB @ 10Gbps | $23.90/月 | [查看 AN5 Tier 1 档位](https://www.dmit.io/cart.php?region=los-angeles&generation=an5&network=tier-1&aff=12046) |
| AN5.T1.V4C4G（VOLUME） | 4 核 / 4GB / 120GB | 20000GB @ 10Gbps | $36.90/月 | [查看 AN5 Tier 1 档位](https://www.dmit.io/cart.php?region=los-angeles&generation=an5&network=tier-1&aff=12046) |
| AN5.T1.G2C4G（GENERAL） | 2 核 / 4GB / 80GB | 4000GB @ 10Gbps | $16.90/月 | [查看 AN5 Tier 1 档位](https://www.dmit.io/cart.php?region=los-angeles&generation=an5&network=tier-1&aff=12046) |
| AN5.T1.G4C8G（GENERAL） | 4 核 / 8GB / 160GB | 8000GB @ 10Gbps | $36.90/月 | [查看 AN5 Tier 1 档位](https://www.dmit.io/cart.php?region=los-angeles&generation=an5&network=tier-1&aff=12046) |

AN4（EPYC 9004）目前主要以 Tier 1 形式在售，是洛杉矶的入门价位段，年付 $36.90 起：

| 套餐 | CPU / 内存 / SSD | 流量 @ 带宽 | 价格 | 购买 |
| --- | --- | --- | --- | --- |
| LAX.AN4.T1.WEE | 1 核 / 1GB / 20GB | 1000GB @ 4Gbps | $36.90/年 | [查看 AN4 Tier 1 档位](https://www.dmit.io/cart.php?region=los-angeles&generation=an4&network=tier-1&aff=12046) |
| LAX.AN4.T1.TINY | 1 核 / 1GB / 20GB | 2000GB @ 4Gbps | $6.90/月 | [查看 AN4 Tier 1 档位](https://www.dmit.io/cart.php?region=los-angeles&generation=an4&network=tier-1&aff=12046) |
| LAX.AN4.T1.STARTER | 1 核 / 2GB / 40GB | 4000GB @ 10Gbps | $12.90/月 | [查看 AN4 Tier 1 档位](https://www.dmit.io/cart.php?region=los-angeles&generation=an4&network=tier-1&aff=12046) |
| LAX.AN4.T1.MINI | 2 核 / 2GB / 60GB | 8000GB @ 10Gbps | $21.90/月 | [查看 AN4 Tier 1 档位](https://www.dmit.io/cart.php?region=los-angeles&generation=an4&network=tier-1&aff=12046) |
| LAX.AN4.T1.MICRO | 4 核 / 4GB / 80GB | 16000GB @ 10Gbps | $32.90/月 | [查看 AN4 Tier 1 档位](https://www.dmit.io/cart.php?region=los-angeles&generation=an4&network=tier-1&aff=12046) |

AN4 的 Pro / EB 系列此前已全部下架，目前洛杉矶的 Premium 和 Eyeball 主力在 AS3 和 AN5 两个平台上。想要新一代 CPU 又不想为线路溢价买单的，AN5 的 Tier 1 是个折中方案。

## 香港和东京：EPYC 7003 与 9005 两条腿

香港的硬件平台同样分成 AS3（EPYC 7003）和 AN5（EPYC 9005，配 DDR5 ECC）两档。Premium 走 CN2 GIA（AS23764），三网平均延迟可以压到 40ms 出头这个量级；Eyeball 属于成本与大陆访问体验之间的平衡档，移动双程 CMIN2 表现不错。香港档位的单价比洛杉矶高不少，同样 1 核 1GB 的入门款签到 $24.90/月，这是机房位置和 CN2 带宽成本的直接结果。

**香港 Eyeball 官方标注为 Beta，路由可能继续调整，实测结果不能当长期线路承诺用。**如果业务对路由稳定性要求高，不要因为 EB 便宜就把 Premium 换掉。

东京方面，DMIT 提供 Premium 和 Tier 1 两条线，档位命名与洛杉矶一致，但同一配置的单价通常更高——东京 Premium 的 1 核 0.75GB / 15GB 入门款报到 $19.90/月。好处是物理距离近，华东、华北方向的延迟比美西低一档。香港和东京的库存与价格波动更频繁，下单前先在订单页确认。

## 优惠码、计费周期，以及那几个容易踩的坑

**优惠码在结账页验证。** 选好套餐和付款周期后，在订单页填入优惠码点“Validate Code”。DMIT 的码基本都绑定具体产品线和付款周期，拿 LAX 的码去套香港套餐是不会生效的。

**流传最久的是下面这两个，但请务必在结账页验证后再付款：**

- `Lite-Annually-Recur-30OFF` —— 标准网络系列年付，据称 7 折循环
- `Lite-Semi-Annually-Recur-20OFF` —— 标准网络系列半年付，据称 8 折循环

需要说明的是，标准网络系列（原 Lite 系列）已经经过一次改名和调整，最低档也被取消过，所以这两个码是否对所有在售档位仍适用，我无法替你打包票。至于那些带 `2025-XMAS-` 前缀的节日码，属于限时活动码，活动窗口过了通常就失效，不要当成长期可用的通用码来用。

**计费周期方面**，DMIT 支持月付、季付、半年付、年付。周期越长折扣越多，但要注意两点：一是部分新平台套餐会取消月付，最低季付起步；二是循环折扣和一次性折扣不一样，循环折扣每次续费都享受，一次性折扣只在首单生效，下单时看清描述。

**流量是双向计费的。** 上传和下载都计入月流量，跑满后降速到套餐标称的限速值继续跑，不停机、不额外收费。做下载站或者大流量的，把双向计费这一条算进去。

**IP 的问题。** 洛杉矶分配的美国原生 IP 在流媒体解锁上有不错的口碑，但商家不做保证，以实测为准。IP 如果被封，可以走工单申请更换，具体规则和费用以官方服务条款为准，别信口口相传的说法。

## 三类需求，直接对号入座

**只想要便宜的美国落地/中转，海外访问为主。** 直接看 Tier 1，两个候选：`LAX.AS3.T1.WEE` 年付 $36.90，4Gbps 端口、1000GB 流量、超量后还能跑 100Mbps，这是目前 DMIT 最便宜的一个入口；`LAX.AN4.T1.TINY` 月付 $6.90，想要新一点平台又不想年付压钱的就选它。

**移动或联通为主，要流量、预算有限。** Ebeyball 是性价比更高的一档。`LAX.AS3.EB.TINY` 和 `LAX.AS3.Pro.TINY` 都是 $10.90/月，EB 给到的流量多 50%；档位往上走，EB 的流量优势会拉到接近一倍。

**电信为主、跑业务或对晚高峰有要求。** Premium 才是对应档。`LAX.AS3.Pro.Pocket` $16.90/月 是配置和价格的中间点，2 核 2GB、1500GB 流量、4Gbps 端口，做小站、API、代理都够用。真要上生产环境且预算允许，再考虑 AN5 平台——9005 的单核性能和 DDR5 内存带宽确实更高，但多出来的性能对大部分人的日常用途是过剩的，这中间的差价值不值，取决于你是否真的跑得满。

**别忽略一个现实：这些套餐是动态库存。** AS3 是补货产品，AN5 经历过下架返场，热门档位随时可能显示缺货。看到合适的档位、确认了库存和价格，该下手就下手；等库存回补的那段时间，价格往往已经不是原来的价格了。

👉 [前往 DMIT 查看当前在售套餐与库存](https://www.dmit.io/aff.php?aff=12046)
