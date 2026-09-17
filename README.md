# Valheim 专用服务器托管：从选配置到开服的完整指南，含 Sharktech 全套餐价格对比

在 Valheim 里被朋友踢出世界、主机一下线整个存档就冻结——这是大多数人开始搜索 dedicated server hosting 的原因。这篇文章会讲清楚三件事：你到底需要什么配置、Sharktech 的服务器方案值不值那个价、以及拿到服务器之后怎么把 Valheim 跑起来（包括跨平台联机的关键细节）。

## 先弄清楚：Valheim 专用服务器到底需要什么配置

好消息是 Valheim 不算重。根据 Valheim 官方 Wiki 的数据，专用服务器的最低配置是 4 核 2.8 GHz CPU、2 GB 内存、2 GB 存储；推荐配置是 6 核 3.4 GHz 以上、4 GB+ 内存、4 GB+ 存储。一个新世界大约吃 1.8–2.4 GB 内存，之后每个有玩家活动的区域再加 100–300 MB。Steam 社区里多数人的实际经验是 8 GB 内存比较稳妥，10–20 GB 存储空间足够放游戏文件和世界数据。

需要提醒一点：服务器主要跑的是通信中继和世界数据，游戏逻辑大部分由客户端承担。CPU 压力集中在两个场景——开新世界时的地形生成，以及玩家进入未探索区域时的即时生成。所以单核性能比核心数量更值得关心。

另外有两个常被忽略的事实：

- 存档每 20 分钟自动保存一次，保存时需要克隆内存，服务器内存和 CPU 越快，克隆造成的卡顿越短。这在人多的时候会明显影响体验。
- 打了 mod 的服务器（比如 BepInEx 或 Thunderstore 上的东西）对硬件要求会往上抬一截，按推荐配置甚至更高来准备。

这些数字决定了你的搜索方向：一台 4 核 / 8 GB 的 VPS 就能带 5–10 人正常玩；如果你还要在同一台机器上跑多个世界、开 mod 服务或者兼顾其他项目，那才需要往 bare-metal（独立服务器）方向看。

## 便宜的"游戏面板托管"和 VPS / 独立服务器，是两种东西

搜 Valheim server hosting 你会看到两类结果，混在一起很容易选错。

第一类是 GPORTAL、Host Havoc 这类按"每个世界"卖的面板托管，价格大约 $6–$15/月。你付钱，点几下按钮，Valheim 就跑起来了。省心，但你拿到的是面板权限，不是系统权限——mod 想怎么装、防火墙怎么配、能跑几个世界，都由服务商说了算。

第二类是 VPS 或独立服务器。你自己装 Linux、自己跑 SteamCMD、自己管进程。这需要一点命令行基础，但换来的是完整的 root 权限：想开三个世界、装任何 mod、再顺便跑个 Minecraft 服，都不用多付一份"世界费"。

Reddit 上 r/valheim 的讨论基本反映这个格局——有人推荐 Dathost 这种轻量方案，有人推荐 Citadel 这类更便宜的托管商，也有人直接说"我自己在 DigitalOcean 上搭，大概 $15/月"。这类方案之间的比价你可以自己做，而如果你确定要走第二条路（root 权限、自己控制一切），那值得认真看看 Sharktech 这种做裸金属和 VPS 的厂商。

## Sharktech 是什么来头

Sharktech（前身 Sharktech Internet Services）是一家运营了 20 年左右的主机商，主营 bare-metal 独立服务器、VPS 和 OpenStack 云托管，机房分布在美国洛杉矶、拉斯维加斯、丹佛、芝加哥以及荷兰阿姆斯特丹。对游戏用途比较关键的两点：所有服务自带 DDoS 防护（不用额外买防护包），以及 24/7 人工技术支持——不是只在工单里排队的那种。

第三方评价方面可以查到的事实：HostAdvice 给 Sharktech 的综合评分是 9.3/10（其中定价单项 4.6/5），评价中提到它"提供高性能的原始算力，适合需要可定制、高性能独立服务器的用户"。Trustpilot 上样本量较小，13 条评价平均 3.4/5，分歧比较大。官网还挂了几家游戏服务商的证言，比如 Dingdian Network 提到他们的游戏服务器常年被 3–8 Gbps 的 DDoS 攻击 targeting，但在 Sharktech 的网络上没有掉过线。这条属于商家展示的客户证言，参考价值你自己权衡，但对开公开服务器的人来说，DDoS 防护确实是刚需——Valheim 公开服务器被攻击踢人是常见抱怨。

## 套餐怎么选：先想清楚你要跑几个世界

Sharktech 的产品线按层级分，价格跨度很大。给 Valheim 用的话，判断标准很简单：几个人玩、几个世界、mod 不 mod。

**如果只是 5–10 个朋友玩一个原版世界**，一台 Smart VPS 的低配（4 GB 内存那一档，约 $7.95/月起）或者 Public Cloud 的 Small 档就够。VPS 用的是 Xeon Gold 处理器加企业级 NVMe 存储，跑一个 Valheim 世界绑绰有余。

**如果要跑多个世界、mod 服、或者跟其他项目共存**，往 Public Cloud 的 Medium/Large 档（$79/$249 起）或者独立服务器方向走。独立服务器的 10 Gbps 带宽和 300TB/月流量对游戏流量来说非常充裕——Valheim 是 UDP 小包流量，几个世界的带宽消耗连 1 TB 都很难碰到。

**如果要开公开服务器或给社区跑多实例**，那 DDoS 防护和网络质量就比绝对算力重要，Sharktech 的定位（游戏服务商本身就是它的客户群）在这个场景下才真正发挥作用。

下面是官网当前公开展示的全部方案汇总。注意：独立服务器的价格是"起售价"，配置升级（加内存、换 CPU、加盘）会往上加价，具体以购物车页为准；标注"Out of Stock"的型号需要联系销售确认库存。

## Sharktech 全套餐对比表（官网当前展示价格）

| 套餐 | 核心配置 | 价格（起售价，USD） | 计费周期 | 购买链接 |
| --- | --- | --- | --- | --- |
| **Smart VPS**（Proxmox，1 个 IPv4 起） | 2–128 vCPU / 4–256 GB 内存 / 40 GB–2 TB NVMe / 4–304 TB 流量 / 1 Gbps / 60 Gbps DDoS 防护 | $7.95/月（年付约 $3.98/月） | 月付 / 季付 / 半年付 / 年付 | [ 部署 Smart VPS](https://bit.ly/SharKTech) |
| **Public Cloud – Small** | 4–16 vCPU / 8–32 GB 内存 / 多层存储（SSD+HDD+NVMe）/ 20 TB–不限流量 | $39/月 | 按需付费（含固定资源，超出部分按小时计） | [ 查看 Public Cloud Small](https://bit.ly/SharKTech) |
| **Public Cloud – Medium** | 8–32 vCPU / 16–64 GB 内存 | $79/月 | 按需付费 | [ 查看 Public Cloud Medium](https://bit.ly/SharKTech) |
| **Public Cloud – Large** | 32–128 vCPU / 64–256 GB 内存 | $249/月 | 按需付费 | [ 查看 Public Cloud Large](https://bit.ly/SharKTech) |
| **Public Cloud – Enterprise** | 64+ vCPU / 128 GB+ 内存 | $499/月 | 按需付费 | [ 查看 Public Cloud Enterprise](https://bit.ly/SharKTech) |
| **独立服务器 – Dual Xeon E5-2695v4（6×2.5" 托架）** | 36 核 2.1 GHz / 64 GB DDR4 / 2 TB M.2 NVMe / 10 Gbps，300TB/月 | $259/月 | 月 / 季 / 半年 / 年付均有（年付 $2641.8） | [ 下单 Dual Xeon E5-2695v4](https://portal.sharktech.net/cart.php?a=add&pid=741&aff=1611) |
| **独立服务器 – Dual Xeon Gold 6248（3×3.5" 托架）** | 40 核 2.5 GHz / 128 GB DDR4 / 2 TB M.2 NVMe / 10 Gbps，300TB/月 | $299/月 | 月付 / 季付 / 半年付 / 年付（年付 $3049.8） | [ 下单 Dual Xeon Gold 6248](https://portal.sharktech.net/cart.php?a=add&pid=660&aff=1611) |
| **独立服务器 – Dual Xeon Gold 6248（6×2.5" 托架）** | 40 核 2.5 GHz / 128 GB DDR4 / 2 TB NVMe | $309/月 | 月付起 | [ 下单 Gold 6248 (6×2.5")](https://portal.sharktech.net/cart.php?a=add&pid=636&aff=1611) |
| **独立服务器 – Dual Xeon Gold 6246（3×3.5" 托架）** | 24 核 3.3 GHz / 128 GB DDR4 / 2 TB NVMe | $309/月 | 月付起 | [ 下单 Gold 6246](https://portal.sharktech.net/cart.php?a=add&pid=814&aff=1611) |
| **独立服务器 – Dual Xeon Gold 6248（6×U.2 托架）** | 40 核 2.5 GHz / 128 GB DDR4 / 2 TB NVMe / 6×U.2 可扩展 | $329/月 | 月付起 | [ 下单 Gold 6248 (U.2)](https://portal.sharktech.net/cart.php?a=add&pid=766&aff=1611) |
| **独立服务器 – Dual Xeon Gold 6248（8×3.5" + 4×U.2）** | 40 核 / 128 GB / 2 TB NVMe | $389/月 | 月付起 | [ 下单 Gold 6248 (8+4 托架)](https://portal.sharktech.net/cart.php?a=add&pid=664&aff=1611) |
| **独立服务器 – AMD EPYC 7702（10×U.2 托架）** | 64 核 2 GHz / 128 GB DDR4 / 2 TB NVMe | $499/月 | 月付起 | [ 下单 EPYC 7702](https://portal.sharktech.net/cart.php?a=add&pid=729&aff=1611) |
| **独立服务器 – Dual AMD EPYC 7702（12×U.2 托架）** | 128 核 2 GHz / 128 GB DDR4 / 2 TB NVMe | $699/月（当前缺货） | 月付起 | [ 咨询 Dual EPYC 库存](https://bit.ly/SharKTech) |

几个补充说明：

- 所有独立服务器都**免安装费**，且自带 DDoS 防护、管理面板和 24/7 支持。
- 洛杉矶站另外还有几款 64 GB 内存的 E5-2695v4 变体（$269–$389），目前显示缺货，需要联系销售报价，所以表里归并到对应档位说明。
- 同样的配置在丹佛、芝加哥、拉斯维加斯和阿姆斯特丹也有上架，价格可能有差异，下单时可以在购物车里选机房位置。
- Smart VPS 长周期有折扣：季付 75 折、半年付 65 折、年付 5 折（即约 $3.98/月）。
- 部分型号偶尔缺货（官网也说明了硬件短缺原因），下单前如果对交付时间敏感，可以先问一下销售。

想直接看全部机房和当前库存的话，👉 点这里进 Sharktech 官网浏览完整服务器列表。

## 拿到服务器之后：从裸 Linux 到能进世界

这是面板托管和自管方案差距最大的部分。以下流程来自 Iron Gate 官方的 Dedicated Server 指南和 Valheim 官方 Wiki，适用于任何你能拿到 root 权限的服务器（Sharktech 的 VPS 和裸金属都算）。

### 1. 装服务器文件

Linux 下装 SteamCMD，然后跑一行命令就能把 Valheim 服务器拉下来：

bash
steamcmd +force_install_dir /path/to/server +login anonymous +app_update 896690 -beta public validate +quit


如果系统里的 glibc 版本低于 2.29，官方建议用 Docker 跑（服务器自带 `docker_start_server.sh` 脚本），Docker Hub 上也有几个下载量上千万的社区镜像可选。

### 2. 写启动脚本

创建 `valheim.sh`（或复制官方的 `start_server.sh` 再改），核心参数大概长这样：

bash
./valheim_server.x86_64 -name "你的服务器名" -port 2456 -nographics -batchmode \
  -world "世界名" -password "密码" -public 1


几个值得记住的参数：`-saveinterval 1800` 控制存档频率（默认 30 分钟一次）；`-backups 4` 控制备份数；`-crossplay` 加上就启用跨平台后端。

### 3. 端口和防火墙

这是最多人卡住的一步。Valheim 用两个 UDP 端口：2456（游戏端口）和 2457（Steam 查询端口）。在云服务器上你要在管理面板或 iptables 里放行这两个端口的 UDP 入站。

### 4. 用 Ctrl+C 关服

官方文档特意强调：关服务器要用 Ctrl+C 发送信号让它正常退出。直接杀进程或点掉窗口，正在进行的世界状态可能没写进磁盘——这正是很多人"进度回档"的原因。

## 跨平台联机：一个参数的差别，体验差很多

如果你队友里有 Xbox 玩家（Valheim 已支持 Xbox Game Pass 和主机版），这里有个直接决定体验的选择：

**不加 `-crossplay`**：走 Steam 后端，玩家直连你的服务器。延迟低、最稳定，但只有 Steam 玩家能进，而且需要你自己搞定端口转发（云服务器上没问题，家用宽带要处理路由器）。

**加 `-crossplay`**：走 Microsoft PlayFab 中继，Steam、Xbox、甚至 Apple Game Center 玩家都能进，而且不需要端口转发——中继替你处理了网络问题。代价是多了一跳，官方 Wiki 明确提到 Crossplay 模式下玩家"更容易遇到延迟、超时和掉线"，且对地理位置更敏感。

还有一个细节：Xbox 玩家不能自己开 dedicated server，但可以加入任何跨平台后端的服务器。所以如果你的固定队伍是 PC + Xbox 混编，`-crossplay` 是唯一选项，这时服务器选个离大家都近的机房（比如都在北美就选洛杉矶/丹佛，欧洲队伍选阿姆斯特丹）比堆硬件更有用。Sharktech 五个机房正好覆盖了这两个区域。

另外提一下 CGNAT 的情况：如果你打算用家用宽带的 PC 免费开服，但 ISP 用了运营商级 NAT，直连模式基本走不通，只能靠 Crossplay 的中继救场——这也是很多"在家开服失败"的人最后去搜 hosting 的原因之一。

## 管理、备份和 mod

服务器跑起来之后，日常管理主要围绕三个文件：`adminlist.txt`、`bannedlist.txt`、`permittedlist.txt`，都在存档目录下，一行一个平台用户 ID。注意 `permittedlist.txt` 一旦启用就是白名单模式，没列进去的人全进不来。游戏内按 F5 可以用 `kick` / `ban` 等管理命令。

世界数据由两个文件构成：`.db`（世界内容）和 `.fwl`（种子等元数据）。备份和迁移必须两个一起、用二进制方式传输，少了 `.fwl` 服务器会直接生成新世界把你的进度抹掉。服务器每 20 分钟会自动产生 `.old` 备份，把后缀去掉就能回滚。

mod 方面，服务器端可以用 r2modman 或 Thunderstore Mod Manager 选 "Valheim Server" 类别来装，BepInEx 是最常用的框架。再强调一次：打 mod 的服务器按官方 Wiki 的说法"需要更好的硬件"，选配置时留点余量。

## 常见问题

**Valheim 专用服务器支持多少人？**

官方没有硬性人数上限，实际瓶颈在硬件和带宽。按 Wiki 数据，一个原版世界 4 GB 内存的服务器带 10 人左右比较从容；8 GB 可以撑 10 人以上或带 mod。人数再多建议直接看 8 GB+ 内存或独立服务器。

**面板托管和 VPS 哪个划算？**

只跑一个原版世界，$10 左右的面板托管省事；跑两个以上世界、要装 mod、或者服务器还想干别的活，VPS / 云主机的单价摊下来更低，而且资源全归你。

**服务器要一直开着吗？**

Dedicated server 的意义就是 7×24 常驻——你下线了世界照样在跑，农作物照样长，传送门照样亮。不想月月付费的话，Steam 里的 "Valheim Dedicated Server" 工具可以在自己 PC 上免费跑一个，代价是电脑不能关机，且家用网络条件要过关。

**怎么把朋友拉进来？**

Steam 后端的服务器会出现在社区服务器列表；也可以直接给对方 IP:端口用 "Join IP" 连。Crossplay 服务器则用 Join Code 或 IP 加端口。记住密码就是启动脚本里 `-password` 设的那个。

**Sharktech 适合开公开 Valheim 服务器吗？**

它的卖点和这个场景匹配度不错：自带 DDoS 防护（公开服务器的主要风险）、机房选择多、24/7 支持。但要注意它卖的是基础设施，不是"开箱即用的 Valheim 面板"——开服、更新、mod 都是你自己管。图省事的话面板托管更合适；想要控制权和长期性价比，它这一类更值。

## 收尾建议

选 Valheim 专用服务器托管，先回答两个问题：队伍里有没有 Xbox 玩家，以及你打算跑一个世界还是多个。前者决定你用不用 Crossplay、机房选哪，后者基本决定了 VPS 和独立服务器之间的分界线。配置上记住那个大致基准：原版 5–10 人，4–8 GB 内存足够；mod 或多世界，按 8 GB 以上准备。价格方面，Sharktech 从 $7.95/月的 VPS 到 $259/月起步的裸金属覆盖了这两个区间，且所有方案都含 DDoS 防护和 24/7 支持，具体下单前记得确认目标型号的库存和机房。

👉 准备好了就去 Sharktech 官网挑一台开服吧。
