---
title: CoNDIS 微型端口驱动程序注册
description: CoNDIS 微型端口驱动程序注册
ms.assetid: 2dfd3bdc-b7b1-4491-b05e-2e8e1f5895b8
keywords:
- 微型端口驱动程序 WDK 网络的 CoNDIS
- NDIS 微型端口驱动程序 WDK CoNDIS
- 注册微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e8c558c2109fc0490edc914f61a344587807e21
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379218"
---
# <a name="condis-miniport-driver-registration"></a>CoNDIS 微型端口驱动程序注册





CoNDIS 微型端口驱动程序初始化等其他微型端口驱动程序，还必须注册的 CoNDIS 的其他入口点。 有关微型端口驱动程序初始化的常规信息，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

若要注册的 CoNDIS 入口点*MiniportXxx*函数、 CoNDIS 微型端口驱动程序调用[ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)函数从[*MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数。 在中*MiniportSetOptions*，微型端口驱动程序初始化[ **NDIS\_微型端口\_共同\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_co_characteristics)结构，并将其在传递*OptionalHandlers*的参数**NdisSetOptionalHandlers**。

微型端口的调用管理器 (MCMs) 还 register *ProtocolXxx*中的函数*MiniportSetOptions*。 有关 MCM 驱动程序注册的详细信息，请参阅[CoNDIS MCM 注册](condis-mcm-registration.md)。

有关配置可选的微型端口驱动程序服务的详细信息，请参阅[配置可选的微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)。

 

 





