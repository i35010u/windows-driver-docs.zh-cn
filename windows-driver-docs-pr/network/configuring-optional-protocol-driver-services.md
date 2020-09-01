---
title: 配置可选的协议驱动程序服务
description: 配置可选的协议驱动程序服务
ms.assetid: 3bb6d0ed-bc44-48c6-8f28-d861c4ff7a87
keywords:
- 协议驱动程序 WDK 网络，可选服务
- NDIS 协议驱动程序 WDK，可选服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a95f237d8d08209b841ab013b8bfdf0f23459ca2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207633"
---
# <a name="configuring-optional-protocol-driver-services"></a>配置可选的协议驱动程序服务





NDIS 调用协议驱动程序的 [*ProtocolSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options) 函数，以允许协议驱动程序配置可选服务。 NDIS 在协议驱动程序调用[**NdisRegisterProtocolDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)函数的上下文中调用*ProtocolSetOptions*

*ProtocolSetOptions* 注册可选 *ProtocolXxx* 函数的默认入口点，并可分配其他驱动程序资源。 若要注册可选的 *ProtocolXxx* 函数，协议驱动程序将调用 [**NdisSetOptionalHandlers**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers) 函数并在 *OptionalHandlers* 参数传递特征结构。 在这种情况下，协议驱动程序会在**NdisSetOptionalHandlers**的*NdisHandle*参数上传递*ProtocolSetOptions*的*NdisDriverHandle*参数中的句柄。

协议驱动程序还可以从[*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数或[*ProtocolOpenAdapterCompleteEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_open_adapter_complete_ex)函数中调用**NdisSetOptionalHandlers** ，之后，协议驱动程序具有来自[**NdisOpenAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)函数的有效句柄。 在这种情况下，协议驱动程序会在**NdisSetOptionalHandlers**的*NdisHandle*参数上传递**NdisOpenAdapterEx**的*NdisBindingHandle*参数中的句柄。

在这种情况下，有效的特征结构包括：

[**NDIS \_ 协议 \_ 共同 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_co_characteristics)

[**NDIS \_ 联合 \_ 客户端 \_ 可选 \_ 处理程序**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_client_optional_handlers)

[**NDIS \_ 联合 \_ 呼叫 \_ 管理器 \_ 可选 \_ 处理程序**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)

NDIS \_ 客户端 \_ 烟囱 \_ 卸载 \_ 一般 \_ 特征 (参阅 [NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md)) 

NDIS \_ 客户端 \_ 烟囱 \_ 卸载 \_ Tcp \_ 特征 (参阅 [NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md)) 

 

