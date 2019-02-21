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
ms.openlocfilehash: 1de340cc58d057ccd4e426bc66f4921e869dd292
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542545"
---
# <a name="condis-mcm-registration"></a>CoNDIS MCM 注册





CoNDIS 微型端口调用管理器 (MCMs) 初始化等其他微型端口驱动程序，还必须注册的 CoNDIS 的其他入口点。 有关微型端口驱动程序初始化的常规信息，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

若要注册的 CoNDIS 入口点*MiniportXxx*函数和*ProtocolXxx*函数、 CoNDIS MCMs 调用[ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)函数从[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)函数。 在中*MiniportSetOptions*，MCM 初始化[ **NDIS\_微型端口\_共同\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565948)结构和传递它在*OptionalHandlers*的参数**NdisSetOptionalHandlers**。

若要注册调用管理器入口点，MCMs 初始化[ **NDIS\_共同\_调用\_MANAGER\_可选\_处理程序**](https://msdn.microsoft.com/library/windows/hardware/ff564883)结构，将在传递*OptionalHandlers*的参数**NdisSetOptionalHandlers**。

有关配置可选的微型端口驱动程序服务的详细信息，请参阅[配置可选的微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)。

 

 





