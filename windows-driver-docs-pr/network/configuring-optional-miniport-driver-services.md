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
ms.openlocfilehash: 709279d522296bde90f27acf90832cd49ae3ffcb
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215254"
---
# <a name="configuring-optional-miniport-driver-services"></a>配置可选的微型端口驱动程序服务





NDIS 调用微型端口驱动程序的 [*MiniportSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options) 函数，以允许该驱动程序配置可选服务。 NDIS 在微型端口驱动程序调用[**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)函数的上下文中调用*MiniportSetOptions* 。

*MiniportSetOptions* 注册可选 *MiniportXxx* 函数的默认入口点，并可分配其他驱动程序资源。 若要注册可选的 *MiniportXxx* 函数，微型端口驱动程序将调用 [**NdisSetOptionalHandlers**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers) 函数并在 *OptionalHandlers* 参数传递特征结构。

从 NDIS 6.0 开始，有效的特征结构包括：

[**NDIS \_ 微型端口 \_ 共同 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_co_characteristics)

[**NDIS \_ 微型端口 \_ PNP \_ 特性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_pnp_characteristics)

[**NDIS \_ 联合 \_ 呼叫 \_ 管理器 \_ 可选 \_ 处理程序**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)

[**NDIS \_提供程序 \_ 烟囱 \_ 卸载 \_ 一般 \_ 特征**](/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_provider_chimney_offload_generic_characteristics) (参阅 [NDIS 6.0 TCP 烟囱卸载文档](full-tcp-offload.md)) 

[**NDIS \_提供程序 \_ 烟囱 \_ 卸载 \_ tcp \_ 特征**](/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_provider_chimney_offload_tcp_characteristics) (参阅 [NDIS 6.0 tcp 烟囱卸载文档](full-tcp-offload.md)) 

从 NDIS 6.30 开始，有效的特征结构还包括以下内容：

[**NDIS \_ 微型端口 \_ SS \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_ss_characteristics)

[**NDIS \_ NDK \_ 提供程序 \_ 特征**](/windows-hardware/drivers/ddi/ndisndk/ns-ndisndk-_ndis_ndk_provider_characteristics)

 

