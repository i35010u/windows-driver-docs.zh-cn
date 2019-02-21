---
title: 移动计划启动
description: 本主题介绍移动计划程序的启动步骤。
ms.assetid: 85671090-C577-4EE7-9113-974E56FF65EB
keywords:
- Windows Mobile 计划启动，请移动计划启动的移动运营商
ms.date: 01/04/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 696c968caf97794db2769963162f4fda81087678
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520246"
---
# <a name="mobile-plans-launch"></a>移动计划启动

[!include[Mobile Plans Beta Prerelease](../mobile-plans-beta-prerelease.md)]

本部分描述了与移动运营商，包括 Web 服务 API 监视、 运行的端到端方案，并查看升级过程已成功启动移动计划所需的工作。

## <a name="before-launch"></a>启动前
你 （移动运营商） 和 Microsoft 将检查所有未处理的问题进行正确寻址移动才能继续进行之前。 因此必须将完全迁移到生产环境。 如果您决定在集成过程中使用的临时终结点，此迁移将需要一周的时间。

## <a name="web-service-api-monitoring"></a>监视 web 服务 API
计划移动服务将使用监视 Web 服务 API 的可用性*Xping*测试执行 ping 操作以确保它两次每分钟，MO 直接门户是可访问。

如果我们未收到预期的响应时间超过 30 分钟，我们将开始升级过程并吸引你的调查。 

## <a name="run-end-to-end-validation"></a>运行端到端验证
Microsoft 必须 esim 卡和/或 SIM ICCID 范围移动计划在生产环境中之前配置起始端到端测试和验证。 此配置将占用一周的时间来实现。 

它是由您来决定是否要升高的测试范围 （完整的生产范围的子集） 的 esim 卡/SIM 范围或完整的生产范围。

端到端验证由你负责，尽管 Microsoft 将支持问题，并帮助相应地解决它们。
以下为建议的最小的方案。 应经过深思熟虑验证您 MO 直接的 web 门户行为。

### <a name="first-run-experience-with-esim"></a>Esim 卡第一次运行的体验

初始的条件：Windows 10 设备不具有 esim 卡配置文件，但它已连接到 internet。

在方案中的步骤：
1. 电话号码查找验证。
2. 启动 MO 直接 web 门户。
3. 完成在门户中的事务。
4. esim 卡配置文件安装和激活。
5. 设备连接。

### <a name="first-run-experience-with-sim"></a>第一次运行的体验 SIM

初始的条件：Windows 10 设备有 SIM。

1. 启动 MO 直接 web 门户。
2. 完成门户中的事务。
3. 设备连接。

## <a name="escalation-process"></a>升级过程

Microsoft 已建立移动运营商和 Microsoft 以任何面向客户的生产事件上协同工作的双向实时站点升级过程。 实时站点问题是不是标准的操作的一部分的任何事件，你的服务或 Microsoft 的服务，并会导致 （或可能会导致） 中断或计划移动体验的质量下降。 在计划移动体验的关键方案是：

- 从而确保计划移动应用可以访问你通过 Walled Garden 或 Wi-fi 或以太网连接的月直接门户。
- 确保用户始终可以使用购买的数据。

此过程的目标是移动运营商和 Microsoft 同意所示：

1. 监视并将下面的过程在本主题中所规定的实时站点事件提升。
2. 之前的事件的升级，将分配正确的优先级使用本主题中所规定的准则。
3. 提供根据关联到设置事件优先级规定在本主题中的最大允许的响应时间的所有事件的响应。

### <a name="live-site-performance-slas"></a>实时站点性能 Sla

下表提供了详细的说明的实时站点性能 Sla，包括服务可用性和预期的关键 Api 的 API 响应时间与移动计划服务集成。

| 服务名称 | 描述 | 发生事件时的影响 | 包括在监视中移动计划 MO API？ | 可用性 | 延迟 |
| --- | --- | --- | --- | --- | --- |
| 核心网络服务 <p>（PGW、 充电的在线系统、 internet 访问权限、 GRX 访问等）</p> | 提供该功能的服务： <ul><li>访问 internet，具有数据限额的用户。</li><li>即使使用任何数据限额的访问封闭范围的。</li></ul> | 用户不能连接到 internet 使用其移动电话网络数据计划。</li></ul> | 否。 <p>移动运营商负责监视其自己的核心网络服务。</p> | 99.90% | 不适用 |
| MO 直接门户 | 一个 web 门户，用户可以访问 MO 直通方案。 | 用户不能以与 MO 直接经验交流，注册数据计划。 | 是 | 99.90% | 400ms |
| xDR <p>(CDR, SDR, TDR)</p> | <ul><li>CDR:调用详细信息记录</li><li>SDR:订阅详细信息记录</li><li>TDR:事务详细信息记录    </li></ul> | 会影响 Microsoft 内部商业智能报告和与移动运营商共享见解 | 否。 <p>移动运营商负责监视其自己 xDR 的服务。</p> | 不适用 | 不适用 |

### <a name="incident-escalation"></a>事件级别呈报

#### <a name="escalation-to-mobile-operators"></a>升级到移动运营商

如果由 Microsoft 检测到的服务中断，则事件将进行会审和处理基于以下严重性表。 对于高严重性事件，Microsoft 的一个存储区操作中心 (OSOC) 将与移动运营商联系。 对于低严重性的事件，Microsoft 计划移动团队将与移动运营商联系。

| 严重性 | 定义 | 通信服务级别协议 |
| --- | --- | --- |
| **高**用户或业务影响。 | 丢失的核心业务方案： <ul><li>服务完全丢失的时间超过 30 分钟 （例如，如果 API 监视测试失败的时间超过 30 分钟）。</li></ul> | 通过电话由 Microsoft OSOC 升级。 <ul><li>1 小时内预期从移动运营商的初始响应。</li><li>不间断的更新应问题解决前每个工作日。</li></ul> |
| **低**用户或业务影响。 | 对非关键的业务方案的影响： <ul><li>报告失败。</li><li>信息请求。</li></ul> | 通过由移动计划团队的电子邮件的升级。 <ul><li>1 个工作日内应从移动运营商的初始响应。</li><li>问题解决前每周应不间断的更新。</li></ul> |

#### <a name="escalation-to-microsoft"></a>上报给 Microsoft

如果检测到的服务中断，可以通过 Microsoft 运营中心提升，并标识为合作伙伴到移动计划服务团队，并且您想要报告的问题。 服务中断的情况包括但不限于已关闭超过 30 分钟，或从计划移动服务接收异常高调用数的移动运营商服务的核心移动计划方案。 你将需要提供用于在操作中心，以确保我们可以进行正确的团队将提供的模板的窗体中事件的详细信息。

- 为高严重性事件上报给 Microsoft 会通过 Microsoft 运营中心在调用 **+1 425-538-9336**和电子邮件至[ osoc@microsoft.com ](mailto:osoc@microsoft.com)。
- 低严重性事件上报给 Microsoft 会通过电子邮件至[ dmcellpd@microsoft.com ](mailto:dmcellpd@microsoft.com)。

### <a name="services-outage"></a>服务中断

#### <a name="microsoft-communication-of-services-outage-to-mobile-operators"></a>Microsoft 的移动运营商的服务中断的通信
Microsoft 将告知任何 Microsoft 网络、 通过电话和电子邮件移动计划或 Microsoft Store 的服务中断的移动运营商不超过 30 分钟后我们首先将此类中断的注意。

#### <a name="mobile-operator-communication-of-services-outage-to-microsoft"></a>移动运营商的 Microsoft 服务中断的通信
你必须告知 Microsoft 任何核心网络服务中断通过电话和电子邮件不能超过 30 分钟后，将首先分别了解此类中断。 所有这类通信应定向到在 Microsoft 运营中心的电话 **+1 425-538-9336**和电子邮件至[ osoc@microsoft.com ](mailto:osoc@microsoft.com)。

#### <a name="planned-maintenance"></a>计划内的维护
定期计划的或例程维护由移动运营商或 Microsoft 移动计划团队操作或可能会产生最终用户影响的服务必须事先进行通信通过此部分中定义的通道。  

#### <a name="communication-of-planned-maintenance-to-mobile-operators"></a>计划内维护移动运营商进行通信
Microsoft 计划在移动团队将晚于事件之前的 5 个工作日内计划内的维护移动运营商无法通信。 完成维护后，将向移动操作员发送通知。

#### <a name="communication-of-planned-maintenance-to-microsoft"></a>向 Microsoft 的执行计划内维护的通信
必须通过电子邮件发送到传递的移动运营商的核心网络服务的定期计划的或例程维护[ osoc@microsoft.com ](mailto:osoc@microsoft.com)不晚于事件之前的 5 个工作日。 维护完成后将通知发送到[ osoc@microsoft.com ](mailto:osoc@microsoft.com)。

#### <a name="requesting-bug-fixes"></a>请求的 bug 修复
**报告 bug** – 每个团队可以通过电子邮件发送到错误报告[ DYNAMOpartnersup@microsoft.com ](mailto:swifipartnersup@microsoft.com)，以及使用它们的对应项，以获取记录的 bug。

**获取已修复 bug** – 移动计划团队必须会审 bug，并提供业务理由/影响。

**部署 bug 修复**– 在 bug 获得批准，若要保持不变，将共享暂定的部署计划和部署修补程序后，将通过电子邮件收到通知的网络提供商。

## <a name="customer-support"></a>客户支持

移动运营商单独负责任何客户支持问题。 