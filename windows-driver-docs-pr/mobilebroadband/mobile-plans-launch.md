---
title: 移动计划启动
description: 本主题介绍移动计划程序的启动步骤。
ms.assetid: 85671090-C577-4EE7-9113-974E56FF65EB
keywords:
- Windows Mobile 计划启动，请移动计划启动的移动运营商
ms.author: windowsdriverdev
ms.date: 03/25/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 437e94786aaa915664a861a75fabdb9f7cf82770
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357739"
---
# <a name="mobile-plans-launch"></a>移动计划启动

本部分描述了与移动运营商，包括 Web 服务 API 监视、 运行的端到端方案，并查看升级过程已成功启动移动计划所需的工作。

## <a name="before-launch"></a>启动前

你 （移动运营商） 和 Microsoft 将检查所有未处理的问题进行正确寻址移动才能继续进行之前。 因此必须将完全迁移到生产环境。

## <a name="launch-validation"></a>启动验证

达成一致的启动日期后，Microsoft 会将移动运营商门户移到生产环境。 移动运营商负责立即执行端到端验证和向 Microsoft 报告任何潜在的问题。 这将使提供支持，以相应地解决问题。

移动 operatosr 是最终负责接受实时、 可在生产服务。

## <a name="after-launch"></a>应用程序启动后

### <a name="api-monitoring"></a>监视 API

计划移动服务将使用监视 Web 服务 API （移动运营商门户） 的可用性*Xping*进行 ping 操作两次每分钟门户，确保它是可访问。

移动计划服务监视的可用性`GetBalance`API 使用定义的协议，两次每分钟，确保它是可访问。 对于这种监视移动运营商应提供可继续使用 ICCID。

### <a name="escalation-process"></a>升级过程

Microsoft 已建立移动运营商和 Microsoft 以任何面向客户的生产事件上协同工作的双向实时站点升级过程。 实时站点问题是不是标准的操作的一部分的任何事件，你的服务或 Microsoft 的服务，并会导致 （或可能会导致） 中断或计划移动体验的质量下降。 在计划移动体验的关键方案是：

- 从而确保计划移动应用可以访问你通过 Walled Garden 或 Wi-fi 或以太网连接的月直接门户。
- 确保用户始终可以使用购买的数据。

此过程的目标是移动运营商和 Microsoft 同意所示：

1. 监视并将实时站点事件遵循本主题中所述的过程提升。
2. 之前的事件的升级，将分配正确的优先级使用本主题中所述的准则。
3. 提供根据关联到事件的优先级，如本主题中所述的最大允许的响应时间的所有事件的响应。

#### <a name="live-site-performance-slas"></a>实时站点性能 Sla

下表提供了详细的说明的实时站点性能 Sla，包括服务可用性和预期的关键 Api 的 API 响应时间与移动计划服务集成。

| 服务名称 | 描述 | 发生事件时的影响 | 包括在监视中移动计划 MO API？ | 可用性 | 延迟 |
| --- | --- | --- | --- | --- | --- |
| 核心网络服务 <p>（PGW、 充电的在线系统、 internet 访问权限、 GRX 访问等）</p> | 提供该功能的服务： <ul><li>访问 internet，具有数据限额的用户。</li><li>访问 Walled Garden 甚至提供任何数据限额。</li></ul> | 用户不能连接到 internet 使用其移动电话网络数据计划。</li></ul> | 否。 <p>移动运营商负责监视其自己的核心网络服务。</p> | 99.90% | 不可用 |
| MO 直接门户 | 一个 web 门户，用户可以访问 MO 直通方案。 | 用户不能以与 MO 直接经验交流，注册数据计划。 | 是 | 99.90% | 400ms |
| xDR <p>(CDR, SDR, TDR)</p> | <ul><li>CDR:调用详细信息记录</li><li>SDR:订阅详细信息记录</li><li>TDR:事务详细信息记录</li></ul> | 会影响 Microsoft 内部商业智能报告和与移动运营商共享见解 | 否。 <p>移动运营商负责监视其自己 xDR 的服务。</p> | 不可用 | 不可用 |

### <a name="incident-escalation"></a>事件级别呈报

#### <a name="escalation-to-mobile-operators"></a>升级到移动运营商

如果由 Microsoft 检测到的服务中断，则该事件是会审和处理基于以下严重级别。

| 严重性 | 业务影响 | 阈值 | 预期的解决时间 | 更新的频率 |
| --- | --- | --- | --- | --- |
| **1** | **中断/灾难：** 发出通过影响力大的影响到单个的合作伙伴或中等或更高版本的总体全局流量量的所有流量。 | 合作伙伴失败百分比 = 100%或全局失败百分比 > 5% | 8 小时 | 建立合作伙伴联系后，应提供电子邮件更新每隔 2 小时 |
| **2** | **服务中断：** 中等程度的影响，为单个的合作伙伴，但仍然较低的整体全局流量数影响大量的用户流量的问题。 | 合作伙伴失败百分比 = 75%或全局失败百分比 = 1%到 5% | 24 小时 | 建立合作伙伴联系后，应提供电子邮件更新每 6 小时 |
| **3** | **标准升级：** 发出低到中等的影响，影响的用户流量在单个伙伴的中等量，但非常低的整体全局流量数。 | 合作伙伴失败百分比 = 25%-75%或全局失败百分比 < 1%或 12 次连续 xPing 测试到 MO 的获取平衡的终结点会失败 （管理包使一个 xPing 调用每 5 分钟） | 最大努力 | 根据需要建立合作伙伴联系后，应提供电子邮件更新 |

#### <a name="escalation-to-microsoft"></a>上报给 Microsoft

如果检测到的服务中断，可升级移动计划服务团队。 服务中断的情况包括但不限于已关闭超过 30 分钟，或从计划移动服务接收异常高调用数的移动运营商服务的核心移动计划方案。

暂存期间的事件 / 载入，升级至[Mobile 计划实现支持](mailto:mpimplementation@microsoft.com)。 有关事件发布载入，升级至[移动计划操作支持](mailto:DYNAMOPARTNERSUP@microsoft.com)。

### <a name="services-outage"></a>服务中断

#### <a name="microsoft-communication-of-services-outage-to-mobile-operators"></a>Microsoft 的移动运营商的服务中断的通信

Microsoft 将告知任何 Microsoft 网络移动计划服务中断通过电子邮件的移动运营商不超过 30 分钟后我们首先将此类中断的注意。

#### <a name="mobile-operator-communication-of-services-outage-to-microsoft"></a>移动运营商的 Microsoft 服务中断的通信

您必须通知 Microsoft 通过电子邮件的任何核心网络服务中断不超过 30 分钟后，将首先分别了解此类中断。 [移动计划操作支持](mailto:DYNAMOPARTNERSUP@microsoft.com)

##### <a name="planned-maintenance"></a>计划内的维护

定期计划的或例程维护由移动运营商或 Microsoft 移动计划团队操作或可能会产生最终用户影响的服务必须事先进行通信通过此部分中定义的通道。  

##### <a name="communication-of-planned-maintenance-to-mobile-operators"></a>计划内维护移动运营商进行通信

Microsoft 计划在移动团队将晚于事件之前的 5 个工作日内计划内的维护移动运营商无法通信。 完成维护后，通知发送到移动运营商。

##### <a name="communication-of-planned-maintenance-to-microsoft"></a>向 Microsoft 的执行计划内维护的通信

定期计划的或例程维护移动运营商的核心网络服务必须通过传递给 Microsoft 的电子邮件不晚到事件之前的 5 个工作日[移动计划操作支持](mailto:DYNAMOPARTNERSUP@microsoft.com)。

##### <a name="requesting-bug-fixes"></a>请求的 bug 修复

**报告 bug** – 每个团队可以通过电子邮件发送到错误报告[移动计划操作支持](mailto:DYNAMOPARTNERSUP@microsoft.com)，以及使用它们的对应项，以获取记录的 bug。

### <a name="customer-support"></a>客户支持

移动运营商单独负责任何客户支持问题。