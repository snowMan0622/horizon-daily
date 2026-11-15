---
layout: default
title: "Horizon Summary: 2026-11-15 (ZH)"
date: 2026-11-15
lang: zh
---

> 从 115 条内容中筛选出 6 条重要资讯。

---

**科技新闻**
1. [星舰第 15 次试飞首次用发射塔捕获二级飞船](#item-tech-news-1) ⭐️ 8.0/10
2. [Lovable 生成应用因 RLS 不足泄露护照信息与逾 20 万条私信](#item-tech-news-2) ⭐️ 8.0/10
3. [黄仁勋辞任英伟达 CEO，请愿恢复其职务签名破 12 万](#item-tech-news-3) ⭐️ 8.0/10
4. [Cloudflare 以 Apache 2.0 开源 AI 代理浏览器 Kitesurf](#item-tech-news-4) ⭐️ 8.0/10
5. [特斯拉 Cybercab 订阅协议：月租 299 美元，不订阅无法运行](#item-tech-news-5) ⭐️ 8.0/10
6. [PyPI 新版项目页上线，强化安全与来源信号](#item-tech-news-6) ⭐️ 7.0/10

---

## 科技新闻

<a id="item-tech-news-1"></a>
### [星舰第 15 次试飞首次用发射塔捕获二级飞船](https://www.spacex.com/launches/starship-flight-15) ⭐️ 8.0/10

SpaceX 在星舰第 15 次试飞中首次用发射塔“筷子”机械臂捕获从轨道返回的第二级飞船 Ship 42，这是轨道级火箭上面级首次被送回发射场并由发射塔捕获。飞船于美国中部时间 13 日下午随助推器 B22 从得州星际基地升空，完成约 14 圈轨道飞行后离轨再入，于 11 月 14 日 16:20（北京时间 15 日 5:20）落入机械臂之间，距升空约 22.5 小时。原计划的双捕获未实现：SpaceX 称 B22 返航途中出现低燃料告警，捕获程序取消，助推器改道在墨西哥湾溅落，具体中止原因仍在调查。SpaceX 表示，3 颗卫星搭载的摄像头拍摄显示隔热罩状态良好，因此放弃了备用的海上溅落方案。

hackernews · ls612 · 11月14日 21:22 · [社区讨论](https://news.ycombinator.com/item?id=50500963)

**「背景」** 星舰此前已多次成功用发射塔“筷子”机械臂捕获返回的超重型助推器，但捕获从轨道返回的第二级飞船尚属首次。本次第 15 次试飞原计划让助推器与飞船两级同时返回发射场分别被捕获，最终仅飞船完成塔捕，助推器 B22 因返航途中出现低燃料告警而取消捕获、改在墨西哥湾溅落。

**「影响」** SpaceX 称双筷子式抓取是实现高频检查、修复和重新发射的关键，公司很可能在下一次飞船任务中再次尝试捕获。对关注复用成本的人来说，真正的验证点仍是同一艘飞船能否复飞并再次被捕获；本次仅完成捕获，尚未复飞。

**「社区讨论」** 有评论者将星舰类比为“做对了的航天飞机”，认为其助推器完全复用、飞船置于顶部堆叠的设计规避了固体助推器和侧挂构型的历史风险；也有人指出，若隔热罩经得起复用，下一步是双捕获和复飞同一批飞船，届时入轨成本才会显著下降。另有评论提到南海出现类似用交叉钢缆网格回收的装置，属于不同工程路径的同一思路。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.space.com/space-exploration/launches-spacecraft/spacex-chopsticks-catch-starship-upper-stage-flight-14">&#x27;Now everything changes&#x27;: SpaceX catches Starship upper stage ...</a></li>
<li><a href="https://www.cnbc.com/2026/11/14/spacex-plans-to-try-first-ever-catch-of-starship-rocket-from-orbit.html">SpaceX catches upper stage of Starship rocket in historic first</a></li>
<li><a href="https://www.indiatoday.in/science/story/ship-42-returns-from-orbit-and-is-caught-by-starbases-launch-tower-3039186-2026-11-15">SpaceX Starship Flight 15: Ship caught by Chopsticks in ...</a></li>

</ul>
</details>

**标签**: `#spacex`, `#reusable-rockets`, `#aerospace-engineering`, `#hardware`, `#spaceflight`

---

<a id="item-tech-news-2"></a>
### [Lovable 生成应用因 RLS 不足泄露护照信息与逾 20 万条私信](https://www.crissyfield.de/research/lovable-en/) ⭐️ 8.0/10

安全研究人员发现，部分由 Lovable 构建的应用因 Row-Level Security（行级安全）配置不足，暴露了护照信息和超过 20 万条私人消息。Lovable 安全负责人 Igor 在评论中确认，这些应用的根因是 RLS 不足，并称平台会在发布前自动扫描每个应用、提供免费的深度 SAST 扫描，用户可手动选择“Fix”修复或开启后台自动修复，也可阻止发布。该发现来自研究者的博客文章，属于已披露的实际暴露案例，而非厂商的规划声明。

hackernews · armcat · 11月14日 17:43 · [社区讨论](https://news.ycombinator.com/item?id=50499017)

**「背景」** Supabase 的 Postgres 行级安全（RLS）在数据库内执行细粒度授权规则；暴露 schema 中未启用 RLS 的表，任何拥有该表权限的角色都可读写。据外部报道，Supabase 于 10 月 30 日调整了新建 public 表的默认授权行为，但已有项目中的表保留原有授权和 RLS 状态，此前开放的表仍然开放。

**「影响与应对」** 对使用 Lovable 搭配 Supabase 构建应用的开发者而言，这意味着默认配置下的数据表可能对未授权访问开放，需自行核查并收紧 RLS 策略，而不能仅依赖平台扫描。评论者 SOLAR\_FIELDS 指出，Supabase 的相关默认设置据称已于 10 月 30 日修复，但有报告称既有项目仍沿用旧默认值，因此已上线项目应单独验证。

**「社区讨论」** 评论者 SOLAR\_FIELDS 认为 Supabase 也负有责任，称其多年前为降低上手门槛而选择了安全性较弱的默认配置；liquid\_thyme 则主张平台应采用默认拒绝的数据库、最小权限 API 和自动化鉴权测试，让 AI 生成代码难以产生不安全部署。Oras 提出，这类 AI 生成应用数量多、攻击门槛低（仅需在浏览器中检查网络请求），且普通用户难以判断所用应用的风险。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.getleakpatrol.com/supabase-october-30-change.html">Supabase&#x27;s October 30 change: what it fixes for your app&#x27;s ...</a></li>
<li><a href="https://supabase.com/docs/guides/database/postgres/row-level-security">Row Level Security - Supabase Docs</a></li>
<li><a href="https://dev.to/fixloopdev/supabase-oct-30-why-new-tables-get-42501-and-how-to-fix-grants-rls-2i8k">Supabase Oct 30: why new tables get 42501 (and how to fix ...</a></li>

</ul>
</details>

**标签**: `#security`, `#AI-generated code`, `#Row-Level Security`, `#Supabase`, `#data exposure`

---

<a id="item-tech-news-3"></a>
### [黄仁勋辞任英伟达 CEO，请愿恢复其职务签名破 12 万](https://www.ithome.com/1/027/252.htm) ⭐️ 8.0/10

英伟达董事会于 11 月 12 日宣布，黄仁勋辞去总裁、首席执行官及董事会成员职务，即刻生效；执行副总裁兼 CFO 科莱特·克雷斯出任临时 CEO，直至董事会选出正式继任者，并继续兼任原职。随后名为“Stand with Jensen”的请愿要求董事会恢复其 CEO 职务，截至 IT 之家发文已收集超过 12 万个签名，较前一天增长约 6.3 万人次。请愿信由现任员工、前任员工、股东及合作伙伴签署，特斯拉 CEO 埃隆·马斯克也参与签名；组织者称担心黄仁勋可能在未经正当程序的情况下被迫离职。英伟达仍计划于 11 月 17 日太平洋时间约下午 1:20 发布 2027 财年第三季度财报，并于下午 2:00 召开电话会议。

rss · IT之家 · 11月14日 23:18

**「背景」** 英伟达董事会于 11 月 12 日宣布黄仁勋辞去总裁、CEO 及董事会成员职务，即刻生效，由执行副总裁兼 CFO 科莱特·克雷斯出任临时 CEO。此后“Stand with Jensen”请愿迅速扩散，签名人数从约 5 万增至超过 12 万；据 CNBC 报道，两家英伟达大股东也致信董事会，要求考虑包括黄仁勋回归在内的所有领导层方案。

**「影响与关注点」** 临时 CEO 由兼任 CFO 的克雷斯担任，意味着公司财务与日常经营暂时集中于同一人；而 11 月 17 日的财报发布和电话会议将是投资者在 CEO 更替后首次获得公司正式表态的场合。请愿签名规模显示员工、股东与合作伙伴对离职程序存在疑虑，但请愿本身不具约束力，是否恢复职务取决于董事会。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://www.techpowerup.com/354840/open-letter-asking-nvidia-to-reinstate-jensen-huang-passes-115-000-signatures">Open Letter Asking NVIDIA to Reinstate Jensen Huang Passes 115...</a></li>
<li><a href="https://www.cnbc.com/2026/11/14/nvidia-investors-jensen-huang-return-board-letter.html">Nvidia board urged to consider &#x27;potential return of Jensen Huang &#x27;</a></li>

</ul>
</details>

**标签**: `#Nvidia`, `#Jensen Huang`, `#AI hardware`, `#semiconductor industry`, `#corporate governance`

---

<a id="item-tech-news-4"></a>
### [Cloudflare 以 Apache 2.0 开源 AI 代理浏览器 Kitesurf](https://www.phoronix.com/news/Cloudflare-Kitesurf-Open-Source) ⭐️ 8.0/10

Cloudflare 于 11 月 13 日宣布以 Apache 2.0 协议开源面向 AI 智能体的浏览器 Kitesurf，代码已发布在 GitHub。Kitesurf 运行在 Cloudflare Workers 上，无需浏览器容器即可解析 HTML、应用 CSS、执行页面 JavaScript 并完成网页截图渲染，同时支持 Chrome DevTools Protocol，可用现有工具驱动而不依赖任何 Chromium 进程或容器。Cloudflare 表示，它舍弃标签页、主题、扩展和像素级精确渲染等面向人类的功能，聚焦 Token 消耗、上下文窗口、可扩展性、性能与成本；在截图、HTML 提取等任务中 CPU 和内存占用显著低于 Chromium。上述资源对比为官方说法，目前尚无独立基准测试。

telegram · zaihuapd · 11月14日 09:33

**「背景」** Cloudflare 早在 2026 年 8 月就发布了 Kitesurf，当时它作为 Browser Run 中的测试版功能免费提供，定位是运行在 Workers 之上、专为智能体设计的浏览器。此次开源意味着该产品从托管测试服务转为以 Apache 2.0 协议公开代码，开发者可以自行部署和修改。

**「对使用者的影响」** 对需要并发运行大量 AI 代理会话的开发者而言，更低的单会话资源占用意味着同一基础设施上可承载更多并发，并借助 Workers 全球网络按需扩展。由于支持 Chrome DevTools Protocol，已有基于 CDP 的自动化工具链理论上可直接接入，但需注意 Kitesurf 不提供像素级精确渲染等完整浏览器能力，依赖这些特性的任务仍需 Chromium。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://developers.cloudflare.com/browser-run/kitesurf/">Kitesurf · Cloudflare Browser Run docs</a></li>
<li><a href="https://blog.cloudflare.com/kitesurf/">Introducing Kitesurf: The agent-first browser that runs in V8 ...</a></li>

</ul>
</details>

**标签**: `#ai-agents`, `#cloudflare`, `#open-source`, `#web-browsers`, `#serverless`

---

<a id="item-tech-news-5"></a>
### [特斯拉 Cybercab 订阅协议：月租 299 美元，不订阅无法运行](https://www.tesla.com/configurator/api/v4/terms?category=autonomy_subs&amp;amp;locale=en_US&amp;amp;model=cc&amp;amp;saleType=Sale) ⭐️ 8.0/10

特斯拉公布的 Cybercab 自主驾驶订阅协议显示，车辆售价为 29,990 美元，车主须每月支付 299 美元订阅费，否则车辆无法运行。特斯拉可提前一个月通知调价；欠费或违规使用可能导致订阅暂停或取消，累计三次警告则停用自动驾驶一周。协议还规定车辆仅在指定区域运行，未经授权不得接入网约车、配送或租赁平台。上述条款来自一份条款文档的二手摘要，尚未获得独立核实。

telegram · zaihuapd · 11月15日 01:10

**「背景」** Cybercab 是特斯拉面向个人销售的两座自动驾驶车型，其订购页面标价 29,990 美元，并列出每月 299 美元的 Autonomy Subscription 与 1,000 美元不可退订金，预计 2026 年 12 月在得克萨斯州奥斯汀交付。特斯拉官方订阅条款明确写明，车辆在没有有效 Autonomy Subscription 的情况下无法运行，且特斯拉可不时修改条款。Electrek 指出，Cybercab 与用于 Robotaxi 的 Model Y 使用相同的 AI4 硬件和自动驾驶软件，但面向普通车主的 FSD 仍需人类监督。

**「对车主的影响」** 按协议，购车只是获得硬件，持续使用还取决于每月 299 美元的订阅状态，且调价只需提前一个月通知。有意将车辆投入网约车、配送或租赁的车主需注意，未经授权接入这些平台属于违规使用，可能触发暂停或取消订阅。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://electrek.co/2026/11/14/tesla-cybercab-autonomy-subscription-agreement-terms/">Tesla Cybercab’s autonomy agreement is insane: $299/mo or it ...</a></li>
<li><a href="https://teslanorth.com/2026/11/13/tesla-cybercab-autonomy-subscription-terms/">Tesla Cybercab Terms Require a Paid Monthly Subscription</a></li>
<li><a href="https://www.tesla.com/configurator/api/v4/terms?locale=en_US&amp;model=cc&amp;saleType=Sale&amp;category=autonomy_subs">Subscription Agreement - Tesla</a></li>

</ul>
</details>

**标签**: `#autonomous vehicles`, `#Tesla`, `#subscription model`, `#AI hardware`, `#robotaxi`

---

<a id="item-tech-news-6"></a>
### [PyPI 新版项目页上线，强化安全与来源信号](https://blog.pypi.org/posts/2026-11-06-ui-updates-complete/) ⭐️ 7.0/10

PyPI 已上线重新设计的项目页面，在文件列表等处更清晰地展示安全与来源（provenance）信号。社区示例显示，datasette 的项目页带有 provenance 标记，而 dlt 没有。该更新属于平台界面与信息展示层面的改进，具体校验机制和覆盖范围取决于各项目是否采用相应发布流程。

hackernews · rbanffy · 11月14日 15:40 · [社区讨论](https://news.ycombinator.com/item?id=50497892)

**「背景」** PyPI 此前已引入基于 Sigstore 的发布证明（attestations）与 Trusted Publishing 机制：发布者可通过可验证的机器身份（如 GitHub Actions 工作流）在发布时生成签名证明，供他人核验来源。此次改版是把这些已有的来源与安全信号更直接地展示在项目页面上。

**「实际影响」** 对依赖 PyPI 的开发者而言，项目页现在能直接区分是否附带 provenance 信息，便于在安装前判断包的来源可信度；但评论指出，这类信号主要用于发现原本正常、后来被篡改的项目，并不能识别从一开始就恶意的包。

**「社区讨论」** 有评论者担心，把信任建立在“大云厂商”的 OIDC 与签名基础设施上会加剧中心化和锁定，认为这与 Python 社区风格不符；也有人支持推广 Sigstore 式无密钥短时签名，希望更多第三方 CI/CD 服务跟进。另有用户呼吁 trusted publishing 尽快支持可复用工作流（reusable workflows）。

<details><summary>参考链接</summary>
<ul>
<li><a href="https://malware.news/t/attestations-a-new-generation-of-signatures-on-pypi/88434">Attestations : A new generation of signatures on PyPI - Malware News...</a></li>
<li><a href="https://docs.pypi.org/attestations/publish/v1/">PyPI Publish Attestation (v1) - PyPI User Documentation</a></li>

</ul>
</details>

**标签**: `#supply-chain-security`, `#pypi`, `#provenance`, `#sigstore`, `#open-source`

---