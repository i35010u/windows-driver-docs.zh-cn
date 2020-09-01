---
title: ReportDiscoveredTargets2
description: ReportDiscoveredTargets2
ms.assetid: 2845cfa9-a85c-45d4-a962-8f409e96ccec
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e98611009a616f65c0c89bbe510b2aaf4f52f488
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191118"
---
# <a name="reportdiscoveredtargets2"></a>ReportDiscoveredTargets2


**ReportDiscoveredTargets2** WMI 方法报告所有发现的目标。

此 WMI 方法属于 MSiSCSI*中定义*的未发布的[ \_ DiscoveryOperations WMI 类](msiscsi-discoveryoperations-wmi-class.md)。 有关 **ReportDiscoveredTargets2** 方法的参数的说明，请参阅 [**ReportDiscoveredTargets2 \_ OUT**](/windows-hardware/drivers/ddi/iscsifnd/ns-iscsifnd-_reportdiscoveredtargets2_out) 结构的成员说明。

**ReportDiscoveredTargets2** 类似于 [ReportDiscoveredTargets](reportdiscoveredtargets.md) 方法，但 **ReportDiscoveredTargets2** 报告 **ReportDiscoveredTargets** 方法未报告的目标门户信息，如门户组的标记编号。

实现 MSiSCSI DiscoveryOperations WMI 类的微型端口驱动程序 \_ 必须支持 **ReportDiscoveredTargets2**。

 

