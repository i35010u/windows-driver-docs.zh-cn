---
title: CoNDIS 微型端口驱动程序注册
description: CoNDIS 微型端口驱动程序注册
keywords:
- 微型端口驱动程序 WDK 网络，CoNDIS
- NDIS 微型端口驱动程序 WDK，CoNDIS
- 注册微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 937d478473ec3b013743f8f025534626fac47655
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823953"
---
# <a name="condis-miniport-driver-registration"></a>CoNDIS 微型端口驱动程序注册





CoNDIS 微型端口驱动程序像其他微型端口驱动程序一样初始化，还必须注册其他 CoNDIS 入口点。 有关微型端口驱动程序初始化的一般信息，请参阅 [初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

若要注册 *MiniportXxx* 函数的 CoNDIS 入口点，CoNDIS 微型端口驱动程序从 [*MiniportSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数调用 [**NdisSetOptionalHandlers**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数。 在 *MiniportSetOptions* 中，微型端口驱动程序初始化 [**NDIS \_ 微型端口 \_ 共同 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_co_characteristics)结构，并将其传递到 **NdisSetOptionalHandlers** 的 *OptionalHandlers* 参数。

 (MCMs 的微型端口呼叫管理器还) 在 *MiniportSetOptions* 中注册 *ProtocolXxx* 函数。 有关 MCM 驱动程序注册的详细信息，请参阅 [CONDIS MCM registration](condis-mcm-registration.md)。

有关配置可选微型端口驱动程序服务的详细信息，请参阅 [配置可选微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)。

 

