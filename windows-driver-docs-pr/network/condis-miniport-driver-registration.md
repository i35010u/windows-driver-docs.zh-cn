---
title: CoNDIS 微型端口驱动程序注册
description: CoNDIS 微型端口驱动程序注册
ms.assetid: 2dfd3bdc-b7b1-4491-b05e-2e8e1f5895b8
keywords:
- 微型端口驱动程序 WDK 网络，CoNDIS
- NDIS 微型端口驱动程序 WDK，CoNDIS
- 注册微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 614af331301e3cf57950b23412bbc6d0c80e5504
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212943"
---
# <a name="condis-miniport-driver-registration"></a>CoNDIS 微型端口驱动程序注册





CoNDIS 微型端口驱动程序像其他微型端口驱动程序一样初始化，还必须注册其他 CoNDIS 入口点。 有关微型端口驱动程序初始化的一般信息，请参阅 [初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

若要注册*MiniportXxx*函数的 CoNDIS 入口点，CoNDIS 微型端口驱动程序从[*MiniportSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数调用[**NdisSetOptionalHandlers**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数。 在*MiniportSetOptions*中，微型端口驱动程序初始化[**NDIS \_ 微型端口 \_ 共同 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_co_characteristics)结构，并将其传递到**NdisSetOptionalHandlers**的*OptionalHandlers*参数。

 (MCMs 的微型端口呼叫管理器还) 在*MiniportSetOptions*中注册*ProtocolXxx*函数。 有关 MCM 驱动程序注册的详细信息，请参阅 [CONDIS MCM registration](condis-mcm-registration.md)。

有关配置可选微型端口驱动程序服务的详细信息，请参阅 [配置可选微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)。

 

