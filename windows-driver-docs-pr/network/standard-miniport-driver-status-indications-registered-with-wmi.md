---
title: 已注册到 WMI 的标准微型端口驱动程序状态指示
description: 已注册到 WMI 的标准微型端口驱动程序状态指示
ms.assetid: afebd0a2-c811-4534-9320-02b9292ba81b
keywords:
- 状态指示 WDK 网络 WMI
- WMI WDK 网络、 状态指示
- Windows Management Instrumentation WDK 网络、 状态指示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a4175030b6a55869331f58ad9c0b4752d45fb8e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360759"
---
# <a name="standard-miniport-driver-status-indications-registered-with-wmi"></a>已注册到 WMI 的标准微型端口驱动程序状态指示





NDIS 自动注册 Guid 与 WMI 的微型端口驱动程序指示与的 NDIS 状态指示[ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)或[ **NdisMCoIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex)函数。 有关的一般状态指示列表，请参阅[状态指示](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

如果 WMI 客户端使用 WMI 来接收 NDIS WMI 事件注册，NDIS 转换对应的 NDIS 状态指示 WMI 事件，将对所有已注册的事件的 WMI 客户端报告事件。

NDIS 驱动程序还可以生成自定义状态指示。 有关自定义状态指示和 WMI 的详细信息，请参阅[自定义 Oid 和状态指示](customized-oids-and-status-indications.md)。

 

 





