---
title: CoNDIS 客户端注册
description: CoNDIS 客户端注册
ms.assetid: 335dd117-f6c8-4416-8527-ff64c1a5f3ee
keywords:
- 客户端注册 WDK CoNDIS
- 注册入口点
- 入口点 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 899b880e56b1f87d3a33c18e027e2d2272c44a15
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838194"
---
# <a name="condis-client-registration"></a>CoNDIS 客户端注册





CoNDIS 客户端像其他协议驱动程序一样初始化，还必须注册其他 CoNDIS 入口点。 有关协议驱动程序初始化的一般信息，请参阅[初始化协议驱动程序](initializing-a-protocol-driver.md)。

若要注册*ProtocolXxx*函数的 CoNDIS 入口点，CoNDIS 客户端从[*ProtocolSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数调用[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数。 在*ProtocolSetOptions*中，所有 CoNDIS 协议驱动程序都初始化[**NDIS\_协议\_CO\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_co_characteristics)结构并将其传递到**NdisSetOptionalHandlers**的*OptionalHandlers*参数。

若要指定 CoNDIS 客户端的入口点，协议驱动程序会将[**NDIS\_联\_客户端\_可选的\_处理程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_client_optional_handlers)结构中进行初始化，*并将***其传递到NdisSetOptionalHandlers**。

有关配置可选协议驱动程序服务的详细信息，请参阅[配置可选的协议驱动程序服务](configuring-optional-protocol-driver-services.md)。

 

 





