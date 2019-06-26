---
title: 配置可选的微型端口驱动程序服务
description: 配置可选的微型端口驱动程序服务
ms.assetid: 42fe3863-ded0-4a02-9216-86fa4c167a49
keywords:
- 微型端口驱动程序 WDK 网络 （可选） 服务
- NDIS 微型端口驱动程序 WDK，可选的服务
- MiniportSetOptions
- 特征结构 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cc98cf674fc0a85dfd08d307bc09375fc4ff43a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376779"
---
# <a name="configuring-optional-miniport-driver-services"></a>配置可选的微型端口驱动程序服务





NDIS 调用微型端口驱动程序[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数，以允许驱动程序以配置可选的服务。 NDIS 调用*MiniportSetOptions*微型端口驱动程序的调用的上下文中[ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)函数。

*MiniportSetOptions*注册的默认入口点的可选*MiniportXxx*函数，而可以分配其他驱动程序资源。 若要注册可选*MiniportXxx*函数、 微型端口驱动程序调用[ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)函数，并将传递在特征结构*OptionalHandlers*参数。

从 NDIS 6.0 开始，有效特征结构如下所示：

[**NDIS\_微型端口\_共同\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_co_characteristics)

[**NDIS\_MINIPORT\_PNP\_CHARACTERISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_pnp_characteristics)

[**NDIS\_CO\_调用\_MANAGER\_可选\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)

[**NDIS\_提供程序\_烟囱\_卸载\_泛型\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndischimney/ns-ndischimney-_ndis_provider_chimney_offload_generic_characteristics) (请参阅[NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md))

[**NDIS\_提供程序\_烟囱\_卸载\_TCP\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndischimney/ns-ndischimney-_ndis_provider_chimney_offload_tcp_characteristics) (请参阅[NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md))

从开始 NDIS 6.30，有效特征结构还包括以下任务：

[**NDIS\_微型端口\_SS\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_ss_characteristics)

[**NDIS\_NDK\_PROVIDER\_CHARACTERISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndisndk/ns-ndisndk-_ndis_ndk_provider_characteristics)

 

 





