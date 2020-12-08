---
title: NDIS 配置函数
description: NDIS 配置函数
keywords:
- 配置函数 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e11bbd3b4aa2a334b2e4173081d337a0d4564ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841169"
---
# <a name="ndis-configuration-functions"></a>NDIS 配置函数





NDIS 包括以下函数以简化驱动程序配置：

[**NdisOpenConfigurationEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex)

[**NdisMGetBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetbusdata)

[**NdisMSetBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetbusdata)

若要获取适配器的配置信息，NDIS 微型端口驱动程序将调用 **NdisOpenConfigurationEx** 和 [**NdisReadConfiguration**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)。 驱动程序可以调用 **NdisMGetBusData** 来获取特定于总线的信息。 驱动程序可以调用 **NdisMSetBusData** 来设置特定于总线的信息。

协议驱动程序使用适配器名称的注册表路径来读取特定于驱动程序和基础适配器之间的绑定的配置参数。 NDIS 在对 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex) 函数的调用中提供了注册表路径。 驱动程序可以将此注册表路径传递给 [**NdisOpenProtocolConfiguration**](/previous-versions/windows/hardware/network/ff553683(v=vs.85)) 函数或定向注册表调用。 作为替代方法，驱动程序可以将 *BindParameters* 结构传递到 **NdisOpenConfigurationEx** 函数以读取相同参数。

 

