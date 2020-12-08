---
title: CoNDIS MCM 注册
description: CoNDIS MCM 注册
keywords:
- MCMs WDK 网络，注册 CoNDIS 微型端口呼叫管理器
- 微型端口呼叫管理器 WDK 网络，注册 CoNDIS 微型端口呼叫管理器
- 注册微型端口调用管理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4d94de755693b0385ed7bb8664a159d9e270906
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834385"
---
# <a name="condis-mcm-registration"></a>CoNDIS MCM 注册





CoNDIS 微型端口呼叫管理器 (MCMs) 初始化，如其他微型端口驱动程序，并且还必须注册其他 CoNDIS 入口点。 有关微型端口驱动程序初始化的一般信息，请参阅 [初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

若要为 *MiniportXxx* 函数和 *ProtocolXxx* 函数注册 CoNDIS 入口点，CoNDIS MCMs 从 [*NdisSetOptionalHandlers*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数调用 [**MiniportSetOptions**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数。 在 *MiniportSetOptions* 中，MCM 初始化 [**NDIS \_ 微型端口 \_ 共同 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_co_characteristics)结构，并将其传递到 **NdisSetOptionalHandlers** 的 *OptionalHandlers* 参数。

为了注册调用管理器入口点，MCMs 会初始化 [**NDIS \_ 联合 \_ 调用 \_ 管理器 \_ 可选 \_ 处理程序**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)结构，并将其传递到 **NdisSetOptionalHandlers** 的 *OptionalHandlers* 参数。

有关配置可选微型端口驱动程序服务的详细信息，请参阅 [配置可选微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)。

 

