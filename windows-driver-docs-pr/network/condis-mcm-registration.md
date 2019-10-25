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
ms.openlocfilehash: 95bb6c9e2afdac94f6bcf637827399f6b09b7f3d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838190"
---
# <a name="condis-mcm-registration"></a>CoNDIS MCM 注册





CoNDIS 微型端口呼叫管理器（MCMs）初始化方式与其他微型端口驱动程序相同，还必须注册其他 CoNDIS 入口点。 有关微型端口驱动程序初始化的一般信息，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

若要为*MiniportXxx*函数和*ProtocolXxx*函数注册 CoNDIS 入口点，CoNDIS MCMs 从[*NdisSetOptionalHandlers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数调用[**MiniportSetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数。 在*MiniportSetOptions*中，MCM 将[**NDIS\_微型\_\_端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_co_characteristics)初始化为，并将其传递到**NdisSetOptionalHandlers**的*OptionalHandlers*参数。

为了注册呼叫管理器入口点，MCMs 会将[**NDIS\_的\_调用\_管理\_器初始化为可选\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)结构，并将其传递到 NdisSetOptionalHandlers 的*OptionalHandlers*参数.

有关配置可选微型端口驱动程序服务的详细信息，请参阅[配置可选微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)。

 

 





