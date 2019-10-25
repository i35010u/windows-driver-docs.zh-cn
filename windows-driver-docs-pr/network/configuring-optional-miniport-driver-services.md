---
title: 配置可选的微型端口驱动程序服务
description: 配置可选的微型端口驱动程序服务
ms.assetid: 42fe3863-ded0-4a02-9216-86fa4c167a49
keywords:
- 微型端口驱动程序 WDK 网络，可选服务
- NDIS 微型端口驱动程序 WDK，可选服务
- MiniportSetOptions
- 特征结构 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dafe119e67a0628a678f059bc70b12106d3e540b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835037"
---
# <a name="configuring-optional-miniport-driver-services"></a>配置可选的微型端口驱动程序服务





NDIS 调用微型端口驱动程序的[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数，以允许该驱动程序配置可选服务。 NDIS 在微型端口驱动程序调用[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)函数的上下文中调用*MiniportSetOptions* 。

*MiniportSetOptions*注册可选*MiniportXxx*函数的默认入口点，并可分配其他驱动程序资源。 若要注册可选的*MiniportXxx*函数，微型端口驱动程序将调用[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数并在*OptionalHandlers*参数传递特征结构。

从 NDIS 6.0 开始，有效的特征结构包括：

[ **\_CO\_特性的 NDIS\_微型端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_co_characteristics)

[ **\_PNP\_特性的 NDIS\_微型端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_pnp_characteristics)

[**NDIS\_\_MANAGER\_可选\_处理程序的 CO\_调用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)

[**Ndis\_提供程序\_烟囱\_卸载\_一般\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_provider_chimney_offload_generic_characteristics)（请参阅[NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md)）

[**Ndis\_提供程序\_烟囱\_卸载\_TCP\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_provider_chimney_offload_tcp_characteristics)（请参阅[NDIS 6.0 tcp 烟囱卸载文档](full-tcp-offload.md)）

从 NDIS 6.30 开始，有效的特征结构还包括以下内容：

[**NDIS\_微型\_SS\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_ss_characteristics)

[**NDIS\_NDK\_提供程序\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndisndk/ns-ndisndk-_ndis_ndk_provider_characteristics)

 

 





