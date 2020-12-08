---
title: ReportDiscoveredTargets2
description: ReportDiscoveredTargets2
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 92475133778b0fa4fe592a64cf31296f8fb20ead
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815845"
---
# <a name="reportdiscoveredtargets2"></a>ReportDiscoveredTargets2


**ReportDiscoveredTargets2** WMI 方法报告所有发现的目标。

此 WMI 方法属于 MSiSCSI *中定义* 的未发布的 [ \_ DiscoveryOperations WMI 类](msiscsi-discoveryoperations-wmi-class.md)。 有关 **ReportDiscoveredTargets2** 方法的参数的说明，请参阅 [**ReportDiscoveredTargets2 \_ OUT**](/windows-hardware/drivers/ddi/iscsifnd/ns-iscsifnd-_reportdiscoveredtargets2_out) 结构的成员说明。

**ReportDiscoveredTargets2** 类似于 [ReportDiscoveredTargets](reportdiscoveredtargets.md) 方法，但 **ReportDiscoveredTargets2** 报告 **ReportDiscoveredTargets** 方法未报告的目标门户信息，如门户组的标记编号。

实现 MSiSCSI DiscoveryOperations WMI 类的微型端口驱动程序 \_ 必须支持 **ReportDiscoveredTargets2**。

 

