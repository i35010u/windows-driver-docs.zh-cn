---
title: CoNDIS 呼叫管理程序注册
description: CoNDIS 呼叫管理程序注册
ms.assetid: 63cde3d1-122c-4411-91b6-97e97bdd2df3
keywords:
- 呼叫经理 WDK 网络，CoNDIS
- 注册呼叫管理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89af22a9d73619c8379f752cb23deaab4f65ab1b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835146"
---
# <a name="condis-call-manager-registration"></a>CoNDIS 呼叫管理程序注册





CoNDIS 独立调用管理器将像其他协议驱动程序一样初始化，还必须注册其他 CoNDIS 入口点。 有关协议驱动程序初始化的一般信息，请参阅[初始化协议驱动程序](initializing-a-protocol-driver.md)。

若要注册*ProtocolXxx*函数的 CoNDIS 入口点，调用管理器从[*ProtocolSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数调用[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数。 在*ProtocolSetOptions*中，所有 CoNDIS 协议驱动程序都初始化[**NDIS\_协议\_CO\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_co_characteristics)结构并将其传递到**NdisSetOptionalHandlers**的*OptionalHandlers*参数。

若要为呼叫管理器指定入口点，协议驱动程序会将[**NDIS\_联\_调用\_管理\_器初始化为可选\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)结构，并将其传递到*OptionalHandlers*参数**NdisSetOptionalHandlers**。

微型端口呼叫管理器（MCMs）还注册了呼叫管理器*ProtocolXxx*函数。 有关 MCM 驱动程序注册的详细信息，请参阅[CONDIS MCM registration](condis-mcm-registration.md)。

有关配置可选协议驱动程序服务的详细信息，请参阅[配置可选的协议驱动程序服务](configuring-optional-protocol-driver-services.md)。

 

 





