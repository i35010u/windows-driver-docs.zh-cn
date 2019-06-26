---
title: 初始化微型端口中间驱动程序
description: 初始化微型端口中间驱动程序
ms.assetid: b0beea1f-7374-49e9-9650-0bdb37902469
keywords:
- NDIS 中间层驱动程序 WDK，初始化
- 驱动程序 WDK 的中间连接网络、 初始化
- 初始化中间微型端口驱动程序
- 中间微型端口驱动程序 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4498be2cd4df1cc5072fd28be5df05d41d7f0a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379215"
---
# <a name="initializing-a-miniport-intermediate-driver"></a>初始化微型端口中间驱动程序





中间微型端口驱动程序结合了虚拟设备的微型端口驱动程序、 协议驱动程序和物理设备的微型端口驱动程序。 类似于中间驱动程序微型端口中间驱动程序函数上层的微型端口驱动程序。 此类驱动程序允许中间驱动程序直接与基础的微型端口驱动程序进行通信而不会产生与两个单独的驱动程序可能会导致性能损失。

若要注册其物理微型端口驱动程序，中间微型端口驱动程序调用[ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)函数使用适当的参数，就像任何微型端口驱动程序。 若要注册其虚拟微型端口驱动程序调用**NdisMRegisterMiniportDriver**同样，但使用 NDIS\_中间\_在结构中设置的驱动程序标志*MiniportDriverCharacteristics* 。

每个虚拟或物理设备实例的微型端口中间驱动程序，如果**IMMiniport**注册表项设置为**DWORD:0x0000001**，NDIS 调用[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)为虚拟设备的驱动程序已注册的函数。 否则，NDIS 调用驱动程序的*MiniportInitializeEx*物理设备的驱动程序已注册的函数。

 

 





