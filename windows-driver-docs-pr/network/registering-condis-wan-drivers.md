---
title: 注册 CoNDIS WAN 驱动程序
description: 注册 CoNDIS WAN 驱动程序
ms.assetid: e699d1b0-9dbd-4845-b8e3-e83da20e997c
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 连接网络、 注册
- NdisMRegisterMiniportDriver
- 注册的 CoNDIS WAN 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0ae782bce2b9fa27523ae908308932ab8004012
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364071"
---
# <a name="registering-condis-wan-drivers"></a>注册 CoNDIS WAN 驱动程序





调用的 CoNDIS WAN 微型端口驱动程序或 MCM [ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)从其[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)函数以注册其标准*MiniportXxx* NDIS 的函数。 有关注册的详细信息*MiniportXxx*函数，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

WAN 的 CoNDIS 呼叫管理器是 NDIS 协议驱动程序。 在这种情况下，呼叫管理器调用[ **NdisRegisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff564520)注册其标准*ProtocolXxx*函数。 有关注册 NDIS 协议驱动程序的详细信息，请参阅[初始化协议驱动程序](initializing-a-protocol-driver.md)。 调用管理器初始化和 MCM 初始化其他差异有关的信息，请参阅[差异初始化](differences-in-initialization.md)。

在调用**NdisMRegisterMiniportDriver**提供了 NDIS\_微型端口\_驱动程序\_特征结构从微型端口驱动程序。 必须指定正确的 NDIS 版本数。 有关设置 NDIS 版本编号的详细信息，请参阅[ **NDIS\_微型端口\_驱动程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565958)。

WAN 的 CoNDIS 驱动程序必须指示 NDIS 版本 5.0 或更高版本。

NDIS 6.0 和更高版本的驱动程序必须按如下所示注册的 CoNDIS 回调函数：

-   若要注册的 CoNDIS *ProtocolXxx*并*MiniportXxx*函数，所有的 CoNDIS 驱动程序必须调用[ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)函数。

-   若要注册其 CoNDIS *MiniportXxx*函数、 微型端口驱动程序或微型端口呼叫管理器 (MCM) 必须调用**NdisSetOptionalHandlers**函数从其[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)函数，并将其传递[ **NDIS\_微型端口\_共同\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565948)结构。 若要注册呼叫管理器*ProtocolXxx*函数，还提供了 MCMs [ **NDIS\_CO\_调用\_MANAGER\_可选\_处理程序**](https://msdn.microsoft.com/library/windows/hardware/ff564883)结构。

-   若要注册其 CoNDIS *ProtocolXxx*函数，都必须调用客户端或调用管理器[ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)函数从其[ *ProtocolSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff570269)函数，并且必须提供[ **NDIS\_协议\_共同\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff566817)结构。 客户端还必须提供[ **NDIS\_共同\_客户端\_可选\_处理程序**](https://msdn.microsoft.com/library/windows/hardware/ff564884)结构和调用管理器还必须提供[ **NDIS\_共同\_调用\_MANAGER\_可选\_处理程序**](https://msdn.microsoft.com/library/windows/hardware/ff564883)结构。

有关的 CoNDIS 驱动程序注册的详细信息，请参阅[CoNDIS 注册](condis-registration.md)。

.

 

 





