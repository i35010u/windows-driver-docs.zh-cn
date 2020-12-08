---
title: 移动计划启动
description: 本主题介绍移动计划程序的启动步骤。
keywords:
- Windows Mobile 计划启动，移动计划启动移动运营商
ms.date: 03/25/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 8e865027073f00f3c61b1f9b31861bb001d0d140
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805321"
---
# <a name="mobile-plans-launch"></a>移动计划启动

本部分介绍使用移动运营商成功启动移动计划所需的工作，包括 Web 服务 API 监视、运行端到端方案和评审升级过程。

## <a name="before-launch"></a>启动之前

你 (移动运营商) ，Microsoft 将在移动到现场之前，查看是否已正确解决所有未解决的问题。 这对于完全迁移到生产环境非常重要。

## <a name="launch-validation"></a>启动验证

在议定的启动日期，Microsoft 将移动运营商门户转移到生产环境。 移动运营商负责立即执行端到端验证，并报告给 Microsoft 的任何潜在问题。 这将允许提供支持，以相应地解决问题。

Mobile operatosr 最终负责接受实时的生产内服务。

## <a name="after-launch"></a>启动后

### <a name="api-monitoring"></a>API 监视

移动计划服务通过使用 *Xping* 对门户每分钟执行两次 ping 操作来监视 WEB 服务 API (移动运营商门户) 的可用性，确保它可访问。

移动计划服务 `GetBalance` 使用定义的协议（每分钟两次）监视 API 的可用性，确保它可访问。 对于这种监视，移动运营商应该提供将持续使用的 ICCID。

### <a name="escalation-process"></a>上报流程

Microsoft 为移动运营商确立了一个双向实时站点升级流程，让 Microsoft 共同努力处理任何面向客户的生产事件。 实时站点问题是指不是服务或 Microsoft 服务标准操作的一部分的任何事件，导致 (或可能会导致) 中断或降低移动计划体验的质量。 移动计划体验中的关键方案包括：

- 确保移动计划应用可以通过围墙园或 Wi-Fi 或以太网连接访问 MO 直销门户。
- 确保用户始终可以使用购买的数据。

此过程的目标是移动运营商和 Microsoft 同意以下各项：

1. 按照本主题中所述的过程监视和升级实时站点事件。
2. 在上报事件之前，请使用本主题中所述的指导原则分配正确的优先级。
3. 根据本主题中所述，根据与事件优先级关联的最大允许响应时间，提供针对所有事件的响应。

#### <a name="live-site-performance-slas"></a>实时站点性能 Sla

下表提供了有关实时站点性能 Sla 的详细说明，包括服务可用性和与移动计划服务集成的密钥 Api 的预期 API 响应时间。

| 服务名称 | 描述 | 事件发生时的影响 | 包含在移动计划 MO API 监视中？ | 可用性 | 延迟 |
| --- | --- | --- | --- | --- | --- |
| 核心网络服务 <p> (PGW、在线充电系统、internet 访问、GRX 访问等 ) </p> | 提供以下功能的服务： <ul><li>为具有数据限额的用户访问 internet。</li><li>即使没有数据限制也能访问围墙园。</li></ul> | 用户将不能使用手机网络数据计划连接到 internet。</li></ul> | 不是。 <p>移动运营商负责监视其自己的核心网络服务。</p> | 99.90% | 空值 |
| MO 直接门户 | 一个 web 门户，用户可在其中访问 MO Direct 方案。 | 用户将不能与 MO 直接体验合作来注册数据计划。 | 是 | 99.90% | 400ms |
| xDR <p> (CDR、SDR、TDR) </p> | <ul><li>CDR：呼叫详细信息记录</li><li>SDR：订阅详细信息记录</li><li>TDR：事务详细信息记录</li></ul> | 影响 Microsoft 内部商业智能报表并与移动运营商共享见解 | 不是。 <p>移动运营商负责监视自己的 xDR 服务。</p> | 空值 | 空值 |

### <a name="incident-escalation"></a>事件升级

#### <a name="escalation-to-mobile-operators"></a>升级到移动运营商

如果 Microsoft 检测到服务中断，则会根据以下严重性对事件进行会审和处理。

| 严重性 | 业务影响 | 阈值 | 预期解决时间 | 更新节奏 |
| --- | --- | --- | --- | --- |
| **1** | **停机/灾难：** 对高影响的问题，影响到单个合作伙伴的所有流量，或总体全局流量的中等或更大量。 | 合作伙伴失败百分比 = 100% 或全局失败百分比 > 5% | 8 小时 | 建立合作伙伴联系后，每隔2小时就会提供电子邮件更新 |
| **2** | **服务中断：** 影响中等影响，影响单个合作伙伴的大量用户流量，但仍是总体全局流量的总量。 | 合作伙伴失败百分比 = 75% 或全局失败百分比 = 1% 至5% | 24 小时 | 建立合作伙伴联系后，每隔6小时就会提供电子邮件更新 |
| **3** | **标准升级：** 对低到中等影响的问题，影响单个合作伙伴的中等用户流量量，但总体全局通信量极低。 | 伙伴失败百分比 = 25%-75% 或全局失败百分比 < 1% 或12个连续的 xPing 测试到 MO 的获取平衡终结点失败 (MPS 每5分钟发出一个 xPing 调用)  | 最大努力 | 建立合作伙伴联系后，应根据需要提供电子邮件更新 |

#### <a name="escalation-to-microsoft"></a>升级到 Microsoft

如果检测到服务中断，则可以升级到移动计划服务团队。 服务中断包括但不限于核心移动计划方案处于关闭状态的时间超过30分钟，或者移动运营商的服务从移动计划服务接收到异常的大量调用。

对于过渡/载入过程中的事件，升级到 [移动计划实现支持](mailto:mpimplementation@microsoft.com)。 对于载入后的事件，升级到 [移动计划操作支持](mailto:DYNAMOPARTNERSUP@microsoft.com)。

### <a name="services-outage"></a>服务中断

#### <a name="microsoft-communication-of-services-outage-to-mobile-operators"></a>Microsoft 服务中断与移动运营商的通信

Microsoft 将在我们首次意识到此类中断后，通过电子邮件通知移动运营商任何 Microsoft 网络移动计划服务中断。

#### <a name="mobile-operator-communication-of-services-outage-to-microsoft"></a>移动运营商服务中断与 Microsoft 之间的通信

在你首次意识到此类中断后，你必须通过电子邮件通知 Microsoft 所有核心网络服务中断。 [移动计划操作支持](mailto:DYNAMOPARTNERSUP@microsoft.com)

##### <a name="planned-maintenance"></a>计划内维护

必须事先通过本部分中定义的通道来传达移动运营商运行的或可能具有最终用户影响的 Microsoft 移动计划团队运营的服务或日常维护。  

##### <a name="communication-of-planned-maintenance-to-mobile-operators"></a>计划内维护与移动运营商的通信

在事件发生之前，Microsoft 移动计划团队会将计划内维护传达给移动运营商，不超过五个工作日。 维护完成后，会将通知发送到移动运营商。

##### <a name="communication-of-planned-maintenance-to-microsoft"></a>计划内维护与 Microsoft 的通信

若要定期计划或日常维护移动运营商的核心网络服务，则必须通过电子邮件将其发送给 Microsoft，使其不超过五个工作日，然后再执行 [移动计划操作支持](mailto:DYNAMOPARTNERSUP@microsoft.com)。

##### <a name="requesting-bug-fixes"></a>请求 bug 修复

**报告 bug** –每个团队都可以通过电子邮件向 [移动计划操作支持](mailto:DYNAMOPARTNERSUP@microsoft.com)报告 bug，并使用其对应项来记录错误。

### <a name="customer-support"></a>客户支持

移动运营商只负责满足任何客户支持问题。
