---
title: 注册 CoNDIS WAN 驱动程序
description: 注册 CoNDIS WAN 驱动程序
ms.assetid: e699d1b0-9dbd-4845-b8e3-e83da20e997c
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 连接网络、 注册
- NdisMRegisterMiniportDriver
- 注册的 CoNDIS WAN 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b889f5086ea58cdd5dc442046ce62d09247c8db1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374765"
---
# <a name="registering-condis-wan-drivers"></a>注册 CoNDIS WAN 驱动程序





调用的 CoNDIS WAN 微型端口驱动程序或 MCM [ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)从其[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)函数以注册其标准*MiniportXxx* NDIS 的函数。 有关注册的详细信息*MiniportXxx*函数，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

WAN 的 CoNDIS 呼叫管理器是 NDIS 协议驱动程序。 在这种情况下，呼叫管理器调用[ **NdisRegisterProtocolDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver)注册其标准*ProtocolXxx*函数。 有关注册 NDIS 协议驱动程序的详细信息，请参阅[初始化协议驱动程序](initializing-a-protocol-driver.md)。 调用管理器初始化和 MCM 初始化其他差异有关的信息，请参阅[差异初始化](differences-in-initialization.md)。

在调用**NdisMRegisterMiniportDriver**提供了 NDIS\_微型端口\_驱动程序\_特征结构从微型端口驱动程序。 必须指定正确的 NDIS 版本数。 有关设置 NDIS 版本编号的详细信息，请参阅[ **NDIS\_微型端口\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)。

WAN 的 CoNDIS 驱动程序必须指示 NDIS 版本 5.0 或更高版本。

NDIS 6.0 和更高版本的驱动程序必须按如下所示注册的 CoNDIS 回调函数：

-   若要注册的 CoNDIS *ProtocolXxx*并*MiniportXxx*函数，所有的 CoNDIS 驱动程序必须调用[ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)函数。

-   若要注册其 CoNDIS *MiniportXxx*函数、 微型端口驱动程序或微型端口呼叫管理器 (MCM) 必须调用**NdisSetOptionalHandlers**函数从其[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数，并将其传递[ **NDIS\_微型端口\_共同\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_co_characteristics)结构。 若要注册呼叫管理器*ProtocolXxx*函数，还提供了 MCMs [ **NDIS\_CO\_调用\_MANAGER\_可选\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)结构。

-   若要注册其 CoNDIS *ProtocolXxx*函数，都必须调用客户端或调用管理器[ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)函数从其[ *ProtocolSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数，并且必须提供[ **NDIS\_协议\_共同\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_protocol_co_characteristics)结构。 客户端还必须提供[ **NDIS\_共同\_客户端\_可选\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_client_optional_handlers)结构和调用管理器还必须提供[ **NDIS\_共同\_调用\_MANAGER\_可选\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)结构。

有关的 CoNDIS 驱动程序注册的详细信息，请参阅[CoNDIS 注册](condis-registration.md)。

.

 

 





