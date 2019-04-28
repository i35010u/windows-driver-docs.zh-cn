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
ms.openlocfilehash: 59931c1d6eddabb3638ada77c9f75afa8bc43ea5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346009"
---
# <a name="standard-miniport-driver-status-indications-registered-with-wmi"></a>已注册到 WMI 的标准微型端口驱动程序状态指示





NDIS 自动注册 Guid 与 WMI 的微型端口驱动程序指示与的 NDIS 状态指示[ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)或[ **NdisMCoIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563562)函数。 有关的一般状态指示列表，请参阅[状态指示](https://msdn.microsoft.com/library/windows/hardware/ff570879)。

如果 WMI 客户端使用 WMI 来接收 NDIS WMI 事件注册，NDIS 转换对应的 NDIS 状态指示 WMI 事件，将对所有已注册的事件的 WMI 客户端报告事件。

NDIS 驱动程序还可以生成自定义状态指示。 有关自定义状态指示和 WMI 的详细信息，请参阅[自定义 Oid 和状态指示](customized-oids-and-status-indications.md)。

 

 





