---
title: CoNDIS MCM 注册
description: CoNDIS MCM 注册
ms.assetid: 7dfb86c5-e7b6-4b9d-8f29-a6d247500c3e
keywords:
- MCMs WDK 网络，注册 CoNDIS 微型端口呼叫管理器
- 微型端口呼叫管理器 WDK 网络，注册 CoNDIS 微型端口呼叫管理器
- 注册微型端口调用管理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ab744de710727222e0f097335ca945552549e28
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212951"
---
# <a name="condis-mcm-registration"></a>CoNDIS MCM 注册





CoNDIS 微型端口呼叫管理器 (MCMs) 初始化，如其他微型端口驱动程序，并且还必须注册其他 CoNDIS 入口点。 有关微型端口驱动程序初始化的一般信息，请参阅 [初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

若要为*MiniportXxx*函数和*ProtocolXxx*函数注册 CoNDIS 入口点，CoNDIS MCMs 从[*NdisSetOptionalHandlers*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数调用[**MiniportSetOptions**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数。 在*MiniportSetOptions*中，MCM 初始化[**NDIS \_ 微型端口 \_ 共同 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_co_characteristics)结构，并将其传递到**NdisSetOptionalHandlers**的*OptionalHandlers*参数。

为了注册调用管理器入口点，MCMs 会初始化[**NDIS \_ 联合 \_ 调用 \_ 管理器 \_ 可选 \_ 处理程序**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)结构，并将其传递到**NdisSetOptionalHandlers**的*OptionalHandlers*参数。

有关配置可选微型端口驱动程序服务的详细信息，请参阅 [配置可选微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)。

 

