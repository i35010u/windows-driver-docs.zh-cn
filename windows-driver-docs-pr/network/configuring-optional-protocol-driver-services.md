---
title: 配置可选的协议驱动程序服务
description: 配置可选的协议驱动程序服务
ms.assetid: 3bb6d0ed-bc44-48c6-8f28-d861c4ff7a87
keywords:
- 协议驱动程序 WDK 网络 （可选） 服务
- NDIS 协议驱动程序 WDK，可选的服务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cfd9775323b16b2af7969c9dc21cfcd8de329e7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384724"
---
# <a name="configuring-optional-protocol-driver-services"></a>配置可选的协议驱动程序服务





NDIS 调用协议驱动程序[ *ProtocolSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数，以允许协议驱动程序以配置可选的服务。 NDIS 调用*ProtocolSetOptions*协议驱动程序的调用的上下文中[ **NdisRegisterProtocolDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver)函数

*ProtocolSetOptions*寄存器的默认入口点的可选*ProtocolXxx*函数，而可以分配其他驱动程序资源。 若要注册可选*ProtocolXxx*函数、 协议驱动程序调用[ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)函数，并将传递在特征结构*OptionalHandlers*参数。 在这种情况下，协议驱动程序将传递的句柄从*NdisDriverHandle*的参数*ProtocolSetOptions*处*NdisHandle*参数**NdisSetOptionalHandlers**。

协议驱动程序还可以调用**NdisSetOptionalHandlers**从[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)函数或[ *ProtocolOpenAdapterCompleteEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_open_adapter_complete_ex)协议驱动程序已从有效的句柄后正常[ **NdisOpenAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenadapterex)函数。 在这种情况下，协议驱动程序将传递的句柄从*NdisBindingHandle*的参数**NdisOpenAdapterEx**处*NdisHandle*参数**NdisSetOptionalHandlers**。

在这种情况下，有效特征结构是：

[**NDIS\_协议\_共同\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_protocol_co_characteristics)

[**NDIS\_CO\_客户端\_可选\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_client_optional_handlers)

[**NDIS\_CO\_调用\_MANAGER\_可选\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)

NDIS\_客户端\_烟囱\_卸载\_泛型\_特征 (请参阅[NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md))

NDIS\_客户端\_烟囱\_卸载\_TCP\_特征 (请参阅[NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md))

 

 





