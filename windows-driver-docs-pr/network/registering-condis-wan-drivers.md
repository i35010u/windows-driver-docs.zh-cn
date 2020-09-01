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
ms.openlocfilehash: 508806770187b62556a47eaaaed3bdfa6f43d267
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212009"
---
# <a name="registering-condis-wan-drivers"></a>注册 CoNDIS WAN 驱动程序





CoNDIS WAN 微型端口驱动程序或 MCM 从其[**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数调用[**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) ，以向 NDIS 注册其标准*MiniportXxx*函数。 有关注册 *MiniportXxx* 函数的详细信息，请参阅 [初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

CoNDIS WAN 呼叫管理器是一个 NDIS 协议驱动程序。 因此，调用管理器调用 [**NdisRegisterProtocolDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver) 来注册其标准 *ProtocolXxx* 函数。 有关注册 NDIS 协议驱动程序的详细信息，请参阅 [初始化协议驱动程序](initializing-a-protocol-driver.md)。 有关调用管理器初始化与 MCM 初始化之间的其他差异的信息，请参阅 [初始化中的差异](differences-in-initialization.md)。

对 **NdisMRegisterMiniportDriver** 的调用提供了 \_ 来自微型端口驱动程序的 NDIS 微型端口 \_ 驱动程序 \_ 特征结构。 你必须指定正确的 NDIS 版本号。 有关设置 NDIS 版本号的详细信息，请参阅 [**ndis \_ 微型端口 \_ 驱动程序 \_ 特性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)。

CoNDIS WAN 驱动程序必须指示 NDIS 版本5.0 或更高版本。

NDIS 6.0 和更高版本的驱动程序必须注册 CoNDIS 回调函数，如下所示：

-   若要注册 CoNDIS *ProtocolXxx* 和 *MiniportXxx* 函数，所有 CoNDIS 驱动程序都必须调用 [**NdisSetOptionalHandlers**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers) 函数。

-   若要注册其 CoNDIS *MiniportXxx*函数， (MCM) 的微型端口驱动程序或微型端口调用管理器必须从其[*MiniportSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数调用**NdisSetOptionalHandlers**函数并向其传递[**NDIS \_ 微型端口 \_ 共同 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_co_characteristics)结构。 为了注册调用管理器的 *ProtocolXxx* 函数，MCMs 还提供了 [**NDIS \_ 联合 \_ 调用 \_ 管理器 \_ 可选 \_ 处理程序**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers) 结构。

-   若要注册 CoNDIS *ProtocolXxx*函数，客户端或调用管理器必须从其[*ProtocolSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数调用[**NdisSetOptionalHandlers**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数，并且必须提供[**NDIS \_ 协议 \_ 共同 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_co_characteristics)结构。 客户端还必须提供 [**ndis \_ 联合 \_ 客户端 \_ 可选 \_ 处理程序**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_client_optional_handlers) 结构，调用管理器还必须提供 [**ndis \_ 共同 \_ 调用 \_ 管理器 \_ 可选 \_ 处理程序**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers) 结构。

有关 CoNDIS 驱动程序注册的详细信息，请参阅 [CoNDIS registration](condis-registration.md)。

.

 

