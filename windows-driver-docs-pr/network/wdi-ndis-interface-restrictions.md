---
title: WDI NDIS 接口限制
description: WDI IHV 微型端口驱动程序可以访问 NDIS 和 KMDF 提供的所有功能。
ms.assetid: 08996045-674B-465D-8880-088320770D2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26a4f133287844398b49eccfb3a36ce6ddc6b3ca
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216898"
---
# <a name="wdi-ndis-interface-restrictions"></a>WDI NDIS 接口限制


WDI IHV 微型端口驱动程序可以访问 NDIS 和 KMDF 提供的所有功能。 建议 IHV 驱动程序使用 KMDF 基元尽可能地与操作系统的其余部分通信。 虽然该模型不会限制 IHV 微型端口调用任何 NDIS Api，但 Microsoft WLAN 组件会调用一些 NDIS Api，因此 IHV 驱动程序不应调用它们。

WDI IHV 微型端口驱动程序需要注意有关 NDIS 接口的以下限制。

函数 | 限制 | 替代方法 
---|---|--- 
[**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) | 已禁止 |  [**NdisMRegisterWdiMiniportDriver**](/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver) 
[**NdisMDeregisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver) | 已禁止 |  [**NdisMDeregisterWdiMiniportDriver**](/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismderegisterwdiminiportdriver) 
[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) | 不允许的 **MiniportAttributes** 类型：<br />[**NDIS \_ 微型端口 \_ 适配器 \_ 注册 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)<br />[**NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)<br />[**NDIS \_ 微型端口 \_ 适配器 \_ 本机 \_ 802 \_ 11 \_ 属性**](/previous-versions/windows/hardware/wireless/ff565926(v=vs.85)) | 无。 这些使用 WDI 命令进行查询。 
[**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists) | 已禁止 | 用于指示接收的数据包的 WDI 数据路径接收处理程序。 
[**NdisMSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsendnetbufferlistscomplete) | 已禁止 | 用于完成发送的数据包的 WDI 数据路径发送处理程序。

