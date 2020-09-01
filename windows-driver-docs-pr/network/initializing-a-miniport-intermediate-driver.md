---
title: 初始化微型端口中间驱动程序
description: 初始化微型端口中间驱动程序
ms.assetid: b0beea1f-7374-49e9-9650-0bdb37902469
keywords:
- NDIS 中间驱动程序 WDK，初始化
- 中间驱动程序 WDK 网络，初始化
- 初始化微型端口中间驱动程序
- 微型端口中间驱动程序 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c920ff6dcadd476cee78376c92cd2a17a9b4db29
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206441"
---
# <a name="initializing-a-miniport-intermediate-driver"></a>初始化微型端口中间驱动程序





小型端口中间驱动程序将虚拟设备、协议驱动程序和物理设备的微型端口驱动程序的微型端口驱动程序组合在一起。 微型端口中间驱动程序的功能类似于通过微型端口驱动程序分层的中间驱动程序。 此类驱动程序允许中间驱动程序直接与基础微型端口驱动程序通信，而不会导致可能会导致两个单独的驱动程序的性能损失。

若要注册其物理微型端口驱动程序，小型端口中间驱动程序将使用适当的参数调用 [**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) 函数，就像为任何微型端口驱动程序一样。 为了注册其虚拟小型端口，驱动程序将再次调用 **NdisMRegisterMiniportDriver** ，但在 \_ \_ *MiniportDriverCharacteristics* 的结构中设置了 NDIS 中间驱动程序标志。

对于微型端口中间驱动程序的每个虚拟或物理设备实例，如果 **IMMiniport** 注册表项设置为 **DWORD： 0x0000001**，NDIS 将调用为虚拟设备注册的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数。 否则，NDIS 会调用驱动程序为物理设备注册的驱动程序的 *MiniportInitializeEx* 函数。

 

