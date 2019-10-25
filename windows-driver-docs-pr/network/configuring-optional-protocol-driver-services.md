---
title: 配置可选的协议驱动程序服务
description: 配置可选的协议驱动程序服务
ms.assetid: 3bb6d0ed-bc44-48c6-8f28-d861c4ff7a87
keywords:
- 协议驱动程序 WDK 网络，可选服务
- NDIS 协议驱动程序 WDK，可选服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27151e700a3c0c518b993a20c034aa68f9bd7261
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838181"
---
# <a name="configuring-optional-protocol-driver-services"></a>配置可选的协议驱动程序服务





NDIS 调用协议驱动程序的[*ProtocolSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数，以允许协议驱动程序配置可选服务。 NDIS 在协议驱动程序调用[**NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)函数的上下文中调用*ProtocolSetOptions*

*ProtocolSetOptions*注册可选*ProtocolXxx*函数的默认入口点，并可分配其他驱动程序资源。 若要注册可选的*ProtocolXxx*函数，协议驱动程序将调用[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数并在*OptionalHandlers*参数传递特征结构。 在这种情况下，协议驱动程序会在**NdisSetOptionalHandlers**的*NdisHandle*参数上传递*ProtocolSetOptions*的*NdisDriverHandle*参数中的句柄。

协议驱动程序还可以从[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数或[*ProtocolOpenAdapterCompleteEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_open_adapter_complete_ex)函数中调用**NdisSetOptionalHandlers** ，之后协议驱动程序具有来自[**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)的有效句柄。才能. 在这种情况下，协议驱动程序会在**NdisSetOptionalHandlers**的*NdisHandle*参数上传递**NdisOpenAdapterEx**的*NdisBindingHandle*参数中的句柄。

在这种情况下，有效的特征结构包括：

[**NDIS\_协议\_联\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_co_characteristics)

[**NDIS\_共同\_客户端\_可选的\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_client_optional_handlers)

[**NDIS\_\_MANAGER\_可选\_处理程序的 CO\_调用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)

NDIS\_客户端\_烟囱\_卸载\_一般\_特性（请参阅[NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md)）

NDIS\_客户端\_烟囱\_卸载\_TCP\_特征（请参阅[NDIS 6.0 tcp 烟囱卸载文档](full-tcp-offload.md)）

 

 





