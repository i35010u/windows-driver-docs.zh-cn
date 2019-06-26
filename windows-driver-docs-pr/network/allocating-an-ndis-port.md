---
title: 分配 NDIS 端口
description: 分配 NDIS 端口
ms.assetid: 39c77921-5841-40f5-90ba-0fba89b3b55e
keywords:
- WDK NDIS，分配的端口
- NDIS 端口 WDK，分配
- 分配端口的 NDIS
- 端口 WDK NDIS，最大数目
- NDIS 端口 WDK，最大数目
- 最大端口 WDK NDIS 数
- 端口状态 WDK NDIS
- 分配端口状态 WDK NDIS
- 端口号
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2fe73dfc12faa53c90c5e24edb7e111f4b7922f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382917"
---
# <a name="allocating-an-ndis-port"></a>分配 NDIS 端口





若要分配的微型端口适配器的 NDIS 端口，微型端口驱动程序调用[ **NdisMAllocatePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismallocateport)函数。 **NdisMAllocatePort**是同步和返回后 NDIS 已成功将资源分配的所需的端口。

微型端口驱动程序调用之前**NdisMAllocatePort**，该驱动程序必须调用[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)函数来设置的属性中[ **NDIS\_微型端口\_适配器\_注册\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)结构。 微型端口驱动程序可以调用**NdisMAllocatePort**微型端口适配器调用的后面**NdisMSetMiniportAttributes**返回成功和 NDIS 调用之前[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)函数为该微型端口适配器。

NDIS 始终分配默认端口 （端口零） 以便微型端口驱动程序不应分配默认端口。 NDIS 微型端口驱动程序返回窗体后将释放的默认端口[ *MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)。

NDIS 将微型端口驱动程序调用时的端口分配一个端口号[ **NdisMAllocatePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismallocateport)。 该驱动程序指定端口中的特征[ **NDIS\_端口\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_characteristics)之前驱动程序调用的结构**NdisMAllocatePort**. 当**NdisMAllocatePort**成功返回时， **PortNumber** NDIS 成员\_端口\_特征的*端口特征*参数指定该 NDIS 指派给此端口设置为端口号。

返回从之前[ *MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)，微型端口驱动程序必须调用[ **NdisMFreePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreeport)函数来释放的所有端口，与微型端口适配器相关联。 如果微型端口适配器未初始化，该驱动程序必须调用**NdisMFreePort**若要释放的所有驱动程序分配之前它将返回从端口[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。 有关释放 NDIS 端口的详细信息，请参阅[释放 NDIS 端口](freeing-an-ndis-port.md)。

微型端口驱动程序可以分配的端口的最大数目是 0xffffff。 但是，在实践中，驱动程序将设置基于端口类型和驱动程序应用程序的要求的最大数量。 例如，桥应用程序的端口数是不太可能超过 16。 端口数会更高版本中使用 802.1 x 请求方的端口的访问点和使用虚拟专用网络 (VPN) 端口的 WAN 驱动程序的高得多。

微型端口驱动程序分配一个端口后，端口是已分配状态，并该端口未处于活动状态。 端口不能用于发送和接收数据、 启动状态指示，发出 OID 请求，或启动插即用 (PnP) 事件，直到激活端口。 NDIS 默认端口会自动激活后微型端口驱动程序设置的注册属性中[ **NDIS\_微型端口\_适配器\_注册\_属性** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)结构。 若要请求 NDIS 激活默认端口，微型端口驱动程序可以设置 NDIS\_微型端口\_特性\_控件\_默认\_端口中**AttributeFlags**成员的 NDIS\_微型端口\_适配器\_注册\_属性。

NDIS 将传递到的默认端口的身份验证状态[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)在正常**DefaultPortAuthStates**隶属[**NDIS\_微型端口\_INIT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_init_parameters)结构。 如果微型端口驱动程序控制的默认端口，当微型端口驱动程序激活默认端口时，它可以使用的默认身份验证设置来激活默认端口。 有关激活的默认端口的详细信息，请参阅[激活 NDIS 端口](activating-an-ndis-port.md)。

微型端口驱动程序可以使用 NDIS\_端口\_CHAR\_使用\_默认\_身份验证\_中的设置标志**标志**隶属[**NDIS\_端口\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_characteristics)结构的驱动程序分配和激活的端口。 对于分配的情况，NDIS 到新的端口分配默认身份验证状态，并忽略传递给身份验证状态[ **NdisMAllocatePort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismallocateport)函数。

有关 NDIS 端口状态的详细信息，请参阅[NDIS 端口状态](ndis-port-states.md)。 有关激活端口的详细信息，请参阅[激活 NDIS 端口](activating-an-ndis-port.md)。

 

 





