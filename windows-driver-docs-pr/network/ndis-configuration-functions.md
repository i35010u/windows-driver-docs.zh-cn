---
title: NDIS 配置函数
description: NDIS 配置函数
ms.assetid: 248e08d0-6145-499a-b307-2a5ffbd3733f
keywords:
- 配置函数 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44a4e5f4e5e40654d72392f7d0e307330346a3bd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383602"
---
# <a name="ndis-configuration-functions"></a>NDIS 配置函数





NDIS 包括以下功能，以此简化驱动程序配置：

[**NdisOpenConfigurationEx**](https://msdn.microsoft.com/library/windows/hardware/ff563717)

[**NdisMGetBusData**](https://msdn.microsoft.com/library/windows/hardware/ff563591)

[**NdisMSetBusData**](https://msdn.microsoft.com/library/windows/hardware/ff563670)

若要获取配置信息的适配器，NDIS 微型端口驱动程序调用**NdisOpenConfigurationEx**并[ **NdisReadConfiguration**](https://msdn.microsoft.com/library/windows/hardware/ff564511)。 该驱动程序可以调用**NdisMGetBusData**若要获取特定于总线的信息。 该驱动程序可以调用**NdisMSetBusData**设置特定于总线的信息。

协议驱动程序使用适配器名称的注册表路径读取特定于驱动程序和基础适配器之间的绑定的配置参数。 NDIS 提供了对的调用中的注册表路径[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)函数。 该驱动程序可以将传递到此注册表路径[ **NdisOpenProtocolConfiguration** ](https://msdn.microsoft.com/library/windows/hardware/ff553683)函数或定向注册表调用。 作为替代方法，该驱动程序可以将传递*BindParameters*结构**NdisOpenConfigurationEx**函数来读取相同的参数。

 

 





