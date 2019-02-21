---
title: WDI NDIS 接口限制
description: WDI IHV 微型端口驱动程序有权访问所有 NDIS 和 KMDF 提供的功能。
ms.assetid: 08996045-674B-465D-8880-088320770D2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f81c75d19a1f3a45773116f0f78d1da1617d153
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519925"
---
# <a name="wdi-ndis-interface-restrictions"></a>WDI NDIS 接口限制


WDI IHV 微型端口驱动程序有权访问所有 NDIS 和 KMDF 提供的功能。 建议 IHV 驱动程序的通信尽可能的操作系统的其余部分使用 KMDF 基元。 虽然模型不限制 IHV 微型端口调用任何 NDIS Api，因此 IHV 驱动程序不应调用它们由 Microsoft WLAN 组件调用某些 NDIS Api。

WDI IHV 微型端口驱动程序需要注意的 NDIS 接口上的以下限制。

函数 | 限制 | 替代方法 
---|---|--- 
[**NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654) | 不允许 |  [**NdisMRegisterWdiMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/mt297596) 
[**NdisMDeregisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563578) | 不允许 |  [**NdisMDeregisterWdiMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/mt297595) 
[**NdisMSetMiniportAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff563672) | 不允许使用**MiniportAttributes**类型：<br />[**NDIS\_微型端口\_适配器\_注册\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)<br />[**NDIS\_微型端口\_适配器\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)<br />[**NDIS\_微型端口\_适配器\_本机\_802\_11\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565926) | 无。 这些查询使用 WDI 命令。 
[**NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598) | 不允许 | WDI 数据路径接收处理程序，以指示接收到的数据包。 
[**NdisMSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563668) | 不允许 | WDI 数据路径发送处理程序完成发送的数据包。

 





