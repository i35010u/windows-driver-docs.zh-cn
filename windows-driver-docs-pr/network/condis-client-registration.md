---
title: CoNDIS 客户端注册
description: CoNDIS 客户端注册
ms.assetid: 335dd117-f6c8-4416-8527-ff64c1a5f3ee
keywords:
- 客户端注册 WDK 的 CoNDIS
- 注册入口点
- WDK 网络的入口点
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 418c5bd919bca2119c933d4629888deb7bed0bf5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565440"
---
# <a name="condis-client-registration"></a>CoNDIS 客户端注册





CoNDIS 客户端初始化等其他协议驱动程序，还必须注册的 CoNDIS 的其他入口点。 有关协议驱动程序初始化的常规信息，请参阅[初始化协议驱动程序](initializing-a-protocol-driver.md)。

若要注册的 CoNDIS 入口点*ProtocolXxx*函数，客户端调用的 CoNDIS [ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)函数从[ *ProtocolSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff570269)函数。 在中*ProtocolSetOptions*，所有的 CoNDIS 协议驱动程序初始化[ **NDIS\_协议\_共同\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff566817)结构，将在传递*OptionalHandlers*的参数**NdisSetOptionalHandlers**。

若要指定的 CoNDIS 客户端的入口点，协议驱动程序初始化[ **NDIS\_共同\_客户端\_可选\_处理程序**](https://msdn.microsoft.com/library/windows/hardware/ff564884)结构并将其在传递*OptionalHandlers*的参数**NdisSetOptionalHandlers**。

有关配置可选的协议驱动程序服务的详细信息，请参阅[配置可选协议驱动程序服务](configuring-optional-protocol-driver-services.md)。

 

 





