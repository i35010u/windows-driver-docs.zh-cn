---
title: WDI NDIS 接口限制
description: WDI IHV 微型端口驱动程序有权访问所有 NDIS 和 KMDF 提供的功能。
ms.assetid: 08996045-674B-465D-8880-088320770D2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b61885b461d5c78315be0068a4704a6cd1fbad3e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381155"
---
# <a name="wdi-ndis-interface-restrictions"></a>WDI NDIS 接口限制


WDI IHV 微型端口驱动程序有权访问所有 NDIS 和 KMDF 提供的功能。 建议 IHV 驱动程序的通信尽可能的操作系统的其余部分使用 KMDF 基元。 虽然模型不限制 IHV 微型端口调用任何 NDIS Api，因此 IHV 驱动程序不应调用它们由 Microsoft WLAN 组件调用某些 NDIS Api。

WDI IHV 微型端口驱动程序需要注意的 NDIS 接口上的以下限制。

函数 | 限制 | 替代方法 
---|---|--- 
[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver) | 不允许 |  [**NdisMRegisterWdiMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver) 
[**NdisMDeregisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterminiportdriver) | 不允许 |  [**NdisMDeregisterWdiMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nf-dot11wdi-ndismderegisterwdiminiportdriver) 
[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes) | 不允许使用**MiniportAttributes**类型：<br />[**NDIS\_微型端口\_适配器\_注册\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)<br />[**NDIS\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)<br />[**NDIS\_微型端口\_适配器\_本机\_802\_11\_属性**](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff565926(v=vs.85)) | 无。 这些查询使用 WDI 命令。 
[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists) | 不允许 | WDI 数据路径接收处理程序，以指示接收到的数据包。 
[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsendnetbufferlistscomplete) | 不允许 | WDI 数据路径发送处理程序完成发送的数据包。

 





