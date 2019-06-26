---
title: NDIS 配置函数
description: NDIS 配置函数
ms.assetid: 248e08d0-6145-499a-b307-2a5ffbd3733f
keywords:
- 配置函数 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0229b025dc27fe2859e7e6642fbe77d138024c3b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387280"
---
# <a name="ndis-configuration-functions"></a>NDIS 配置函数





NDIS 包括以下功能，以此简化驱动程序配置：

[**NdisOpenConfigurationEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenconfigurationex)

[**NdisMGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismgetbusdata)

[**NdisMSetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetbusdata)

若要获取配置信息的适配器，NDIS 微型端口驱动程序调用**NdisOpenConfigurationEx**并[ **NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreadconfiguration)。 该驱动程序可以调用**NdisMGetBusData**若要获取特定于总线的信息。 该驱动程序可以调用**NdisMSetBusData**设置特定于总线的信息。

协议驱动程序使用适配器名称的注册表路径读取特定于驱动程序和基础适配器之间的绑定的配置参数。 NDIS 提供了对的调用中的注册表路径[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)函数。 该驱动程序可以将传递到此注册表路径[ **NdisOpenProtocolConfiguration** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553683(v=vs.85))函数或定向注册表调用。 作为替代方法，该驱动程序可以将传递*BindParameters*结构**NdisOpenConfigurationEx**函数来读取相同的参数。

 

 





