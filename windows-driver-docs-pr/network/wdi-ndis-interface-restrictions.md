---
title: WDI NDIS 接口限制
description: WDI IHV 微型端口驱动程序可以访问 NDIS 和 KMDF 提供的所有功能。
ms.assetid: 08996045-674B-465D-8880-088320770D2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18a45fbe5e3c2229e66039f1767ddb1de9464093
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842916"
---
# <a name="wdi-ndis-interface-restrictions"></a>WDI NDIS 接口限制


WDI IHV 微型端口驱动程序可以访问 NDIS 和 KMDF 提供的所有功能。 建议 IHV 驱动程序使用 KMDF 基元尽可能地与操作系统的其余部分通信。 虽然该模型不会限制 IHV 微型端口调用任何 NDIS Api，但 Microsoft WLAN 组件会调用一些 NDIS Api，因此 IHV 驱动程序不应调用它们。

WDI IHV 微型端口驱动程序需要注意有关 NDIS 接口的以下限制。

函数 | 限制 | 其他 
---|---|--- 
[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) | 不允许 |  [**NdisMRegisterWdiMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver) 
[**NdisMDeregisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver) | 不允许 |  [**NdisMDeregisterWdiMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismderegisterwdiminiportdriver) 
[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) | 不允许的**MiniportAttributes**类型：<br />[ **\_适配器\_注册\_特性的 NDIS\_微型端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)<br />[**NDIS\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)<br />[**NDIS\_微型端口\_适配器\_本机\_802\_11\_属性**](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff565926(v=vs.85)) | 无。 这些使用 WDI 命令进行查询。 
[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists) | 不允许 | 用于指示接收的数据包的 WDI 数据路径接收处理程序。 
[**NdisMSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete) | 不允许 | 用于完成发送的数据包的 WDI 数据路径发送处理程序。

 





