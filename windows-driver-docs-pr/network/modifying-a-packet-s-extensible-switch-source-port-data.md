---
title: 修改数据包的可扩展交换机源端口数据
description: 修改数据包的可扩展交换机源端口数据
ms.assetid: 44338441-160C-4CD1-8C0B-27CFBE136910
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47a352c08500542cb8e00e62ea7d79d692ce7c04
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342320"
---
# <a name="modifying-a-packets-extensible-switch-source-port-data"></a>修改数据包的可扩展交换机源端口数据


指定的 HYPER-V 可扩展交换机源端口**SourcePortId**中的成员[ **NDIS\_切换\_转发\_详细\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh598211)结构。 此结构包含在带外 (OOB) 转发的数据包的上下文[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 此上下文的详细信息，请参阅[HYPER-V 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

可扩展的交换机扩展必须遵循以下准则，以便修改数据包的源端口标识符：

-   可扩展的交换机扩展必须调用[ *SetNetBufferListSource* ](https://msdn.microsoft.com/library/windows/hardware/hh598300)修改数据包的源端口。 扩展必须直接修改**SourcePortId**的成员[ **NDIS\_开关\_转发\_详细\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh598211)结构。

-   如果扩展是创建或克隆一个数据包时，它必须调用[ *AllocateNetBufferListForwardingContext* ](https://msdn.microsoft.com/library/windows/hardware/hh598134)函数后它会调用[ **NdisAllocateNetBufferList**](https://msdn.microsoft.com/library/windows/hardware/ff561609). 此函数用于转发数据包的信息的 OOB 数据分配可扩展交换机上下文区域。

    当扩展调用[ *AllocateNetBufferListForwardingContext*](https://msdn.microsoft.com/library/windows/hardware/hh598134)，则**SourcePortId**成员设置为**NDIS\_交换机\_默认值\_端口\_ID**。 这将指定数据包源自而不是传入到可扩展交换机端口的扩展。

    源端口为数据包**NDIS\_切换\_默认\_端口\_ID**为特权的可扩展交换机扩展数据路径处理和受信任的。 此类流量应不会对应用到数据包来自其他源端口的策略中。 例如，源端口标识符的数据包**NDIS\_切换\_默认\_端口\_ID**绕过应用的基础的内置的可扩展交换机策略可扩展交换机的微型端口边缘。 这些策略包括访问控制列表 (Acl) 和服务质量 (QoS)。

    当扩展原始数据包流量时，它应使用的源端口**NDIS\_交换机\_默认\_端口\_ID**尽量少，并仔细。 在大多数情况下，该扩展应修改可扩展交换机上的活动端口的源端口标识符。 这样，该端口将应用于该数据包的策略。

    但是，可能有其中扩展具有要使用的源端口的情况下**NDIS\_交换机\_默认\_端口\_ID**它源自的数据包。 例如，如果该扩展源自已发送到其目标上的物理或虚拟网络，应使用的控制数据包**NDIS\_交换机\_默认\_端口\_ID**的源端口标识符。 这可确保数据包将无法筛选，可扩展交换机驱动程序堆栈中的基础扩展被拒绝。

 

 





