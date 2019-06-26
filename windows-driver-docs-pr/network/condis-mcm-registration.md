---
title: CoNDIS MCM 注册
description: CoNDIS MCM 注册
ms.assetid: 7dfb86c5-e7b6-4b9d-8f29-a6d247500c3e
keywords:
- MCMs WDK 网络，注册的 CoNDIS 微型端口调用管理器
- 微型端口调用注册的 CoNDIS 微型端口调用的管理器 WDK 网络管理器
- 注册微型端口调用管理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d989983df77e069d5d65bebdea05717d3d24e98
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379234"
---
# <a name="condis-mcm-registration"></a>CoNDIS MCM 注册





CoNDIS 微型端口调用管理器 (MCMs) 初始化等其他微型端口驱动程序，还必须注册的 CoNDIS 的其他入口点。 有关微型端口驱动程序初始化的常规信息，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

若要注册的 CoNDIS 入口点*MiniportXxx*函数和*ProtocolXxx*函数、 CoNDIS MCMs 调用[ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)函数从[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数。 在中*MiniportSetOptions*，MCM 初始化[ **NDIS\_微型端口\_共同\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_co_characteristics)结构和传递它在*OptionalHandlers*的参数**NdisSetOptionalHandlers**。

若要注册调用管理器入口点，MCMs 初始化[ **NDIS\_共同\_调用\_MANAGER\_可选\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)结构，将在传递*OptionalHandlers*的参数**NdisSetOptionalHandlers**。

有关配置可选的微型端口驱动程序服务的详细信息，请参阅[配置可选的微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)。

 

 





