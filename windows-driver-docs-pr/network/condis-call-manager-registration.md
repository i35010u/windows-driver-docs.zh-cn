---
title: CoNDIS 呼叫管理程序注册
description: CoNDIS 呼叫管理程序注册
ms.assetid: 63cde3d1-122c-4411-91b6-97e97bdd2df3
keywords:
- 调用的 CoNDIS-网络管理器 WDK
- 注册调用管理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a8b7f870cfe66c8cc3d131ed85b072d8240b0ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379253"
---
# <a name="condis-call-manager-registration"></a>CoNDIS 呼叫管理程序注册





独立的 CoNDIS 调用管理器初始化等其他协议驱动程序，还必须注册的 CoNDIS 的其他入口点。 有关协议驱动程序初始化的常规信息，请参阅[初始化协议驱动程序](initializing-a-protocol-driver.md)。

若要注册的 CoNDIS 入口点*ProtocolXxx*函数，请调用管理器调用[ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)函数从[ *ProtocolSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数。 在中*ProtocolSetOptions*，所有的 CoNDIS 协议驱动程序初始化[ **NDIS\_协议\_共同\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_protocol_co_characteristics)结构，将在传递*OptionalHandlers*的参数**NdisSetOptionalHandlers**。

若要指定调用管理器入口点，协议驱动程序初始化[ **NDIS\_共同\_调用\_MANAGER\_可选\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)结构，并将其在传递*OptionalHandlers*参数**NdisSetOptionalHandlers**。

微型端口的调用管理器 (MCMs) 还注册调用管理器*ProtocolXxx*函数。 有关 MCM 驱动程序注册的详细信息，请参阅[CoNDIS MCM 注册](condis-mcm-registration.md)。

有关配置可选的协议驱动程序服务的详细信息，请参阅[配置可选协议驱动程序服务](configuring-optional-protocol-driver-services.md)。

 

 





