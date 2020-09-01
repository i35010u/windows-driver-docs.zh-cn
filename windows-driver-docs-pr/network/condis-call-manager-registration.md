---
title: CoNDIS 呼叫管理程序注册
description: CoNDIS 呼叫管理程序注册
ms.assetid: 63cde3d1-122c-4411-91b6-97e97bdd2df3
keywords:
- 呼叫经理 WDK 网络，CoNDIS
- 注册呼叫管理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a4cb431186448bb1cfcb3eea3a83e03b4b3629a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217684"
---
# <a name="condis-call-manager-registration"></a>CoNDIS 呼叫管理程序注册





CoNDIS 独立调用管理器将像其他协议驱动程序一样初始化，还必须注册其他 CoNDIS 入口点。 有关协议驱动程序初始化的一般信息，请参阅 [初始化协议驱动程序](initializing-a-protocol-driver.md)。

若要注册*ProtocolXxx*函数的 CoNDIS 入口点，调用管理器从[*ProtocolSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数调用[**NdisSetOptionalHandlers**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数。 在*ProtocolSetOptions*中，所有 CoNDIS 协议驱动程序初始化[**NDIS \_ 协议 \_ 共同 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_co_characteristics)结构，并将其传递到**NdisSetOptionalHandlers**的*OptionalHandlers*参数。

若要为呼叫管理器指定入口点，协议驱动程序将初始化[**NDIS \_ 联合 \_ 调用 \_ 管理器 \_ 可选 \_ 处理程序**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)结构，并将其传递到**NdisSetOptionalHandlers**的*OptionalHandlers*参数。

小型 (MCMs 的小型呼叫管理器还) 注册调用管理器 *ProtocolXxx* 函数。 有关 MCM 驱动程序注册的详细信息，请参阅 [CONDIS MCM registration](condis-mcm-registration.md)。

有关配置可选协议驱动程序服务的详细信息，请参阅 [配置可选的协议驱动程序服务](configuring-optional-protocol-driver-services.md)。

 

