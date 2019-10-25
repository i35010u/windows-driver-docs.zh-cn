---
title: 注册 CoNDIS WAN 驱动程序
description: 注册 CoNDIS WAN 驱动程序
ms.assetid: e699d1b0-9dbd-4845-b8e3-e83da20e997c
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，注册
- NdisMRegisterMiniportDriver
- 注册 CoNDIS WAN 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a054daa802e6654910c945d5d5e761b644229aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842078"
---
# <a name="registering-condis-wan-drivers"></a>注册 CoNDIS WAN 驱动程序





CoNDIS WAN 微型端口驱动程序或 MCM 从其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数调用[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) ，以向 NDIS 注册其标准*MiniportXxx*函数。 有关注册*MiniportXxx*函数的详细信息，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

CoNDIS WAN 呼叫管理器是一个 NDIS 协议驱动程序。 因此，调用管理器调用[**NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)来注册其标准*ProtocolXxx*函数。 有关注册 NDIS 协议驱动程序的详细信息，请参阅[初始化协议驱动程序](initializing-a-protocol-driver.md)。 有关调用管理器初始化与 MCM 初始化之间的其他差异的信息，请参阅[初始化中的差异](differences-in-initialization.md)。

对**NdisMRegisterMiniportDriver**的调用提供一个 NDIS\_微型端口驱动程序\_驱动程序\_特征结构。 你必须指定正确的 NDIS 版本号。 有关设置 NDIS 版本号的详细信息，请参阅[**ndis\_微型端口\_驱动程序\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)。

CoNDIS WAN 驱动程序必须指示 NDIS 版本5.0 或更高版本。

NDIS 6.0 和更高版本的驱动程序必须注册 CoNDIS 回调函数，如下所示：

-   若要注册 CoNDIS *ProtocolXxx*和*MiniportXxx*函数，所有 CoNDIS 驱动程序都必须调用[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数。

-   若要注册 CoNDIS *MiniportXxx*函数，微型端口驱动程序或微型端口调用管理器（MCM）必须从其[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数调用**NdisSetOptionalHandlers**函数并向其传递[**NDIS\_微型端口\_联\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_co_characteristics)结构。 为了注册调用管理器的*ProtocolXxx*函数，MCMs 还提供了一个[**NDIS\_CO\_调用\_manager\_可选\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)结构。

-   若要注册 CoNDIS *ProtocolXxx*函数，客户端或调用管理器必须从其[*ProtocolSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数调用[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数，并且必须[ **\_CO\_提供 NDIS\_协议特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_co_characteristics)结构。 客户端还必须提供[**ndis\_共同\_客户端\_可选的\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_client_optional_handlers)结构和调用管理器还必须提供[**ndis\_联合\_调用\_MANAGER\_可选\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)结构。

有关 CoNDIS 驱动程序注册的详细信息，请参阅[CoNDIS registration](condis-registration.md)。

。

 

 





