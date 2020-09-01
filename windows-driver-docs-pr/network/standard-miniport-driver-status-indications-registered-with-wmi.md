---
title: 已注册到 WMI 的标准微型端口驱动程序状态指示
description: 已注册到 WMI 的标准微型端口驱动程序状态指示
ms.assetid: afebd0a2-c811-4534-9320-02b9292ba81b
keywords:
- 状态指示 WDK 网络，WMI
- WMI WDK 网络，状态指示
- Windows Management Instrumentation WDK 网络，状态指示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fde52825aaa001faa82400bab4c808e937bc8aa0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216554"
---
# <a name="standard-miniport-driver-status-indications-registered-with-wmi"></a>已注册到 WMI 的标准微型端口驱动程序状态指示





NDIS 自动向 WMI 注册 Guid，以获取 NDIS 状态指示，微型端口驱动程序用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) 或 [**NdisMCoIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex) 函数指示。 有关一般状态指示的列表，请参阅 [状态指示](/windows-hardware/drivers/ddi/_netvista/)。

如果 WMI 客户端向 WMI 注册接收 NDIS WMI 事件，NDIS 会将相应的 NDIS 状态指示转换为 WMI 事件，并向所有已注册事件的 WMI 客户端报告该事件。

NDIS 驱动程序还可以生成自定义状态指示。 有关自定义状态指示和 WMI 的详细信息，请参阅 [自定义 oid 和状态指示](customized-oids-and-status-indications.md)。

 

