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
ms.openlocfilehash: 77224e10b1f2d219db37d54b8e608b86cec8b477
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379243"
---
# <a name="condis-client-registration"></a>CoNDIS 客户端注册





CoNDIS 客户端初始化等其他协议驱动程序，还必须注册的 CoNDIS 的其他入口点。 有关协议驱动程序初始化的常规信息，请参阅[初始化协议驱动程序](initializing-a-protocol-driver.md)。

若要注册的 CoNDIS 入口点*ProtocolXxx*函数，客户端调用的 CoNDIS [ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)函数从[ *ProtocolSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数。 在中*ProtocolSetOptions*，所有的 CoNDIS 协议驱动程序初始化[ **NDIS\_协议\_共同\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_protocol_co_characteristics)结构，将在传递*OptionalHandlers*的参数**NdisSetOptionalHandlers**。

若要指定的 CoNDIS 客户端的入口点，协议驱动程序初始化[ **NDIS\_共同\_客户端\_可选\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_client_optional_handlers)结构并将其在传递*OptionalHandlers*的参数**NdisSetOptionalHandlers**。

有关配置可选的协议驱动程序服务的详细信息，请参阅[配置可选协议驱动程序服务](configuring-optional-protocol-driver-services.md)。

 

 





