---
title: HYPER-V 可扩展交换机混合转发
description: 本部分介绍 HYPER-V 可扩展交换机使用的混合转发
ms.assetid: 135CA734-1C92-4EEA-81DC-96A6A68ABBE8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6739599d1f22dffadb2906c10a3353fc29a37c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322126"
---
# <a name="hybrid-forwarding"></a>混合转发


从 NDIS 6.40 （Windows Server 2012 R2 的 HYPER-V 可扩展交换机体系结构支持混合转发可扩展交换机的 HYPER-V 网络虚拟化 (HNV) 组件和转发扩展。

**请注意**  此页面假定您熟悉[使用通用路由封装 (NVGRE) 任务卸载的网络虚拟化](network-virtualization-using-generic-routing-encapsulation--nvgre--task-offload.md)和[的 HYPER-V 可扩展交换机概述](overview-of-the-hyper-v-extensible-switch.md).

 

## <a name="nvgre-and-non-nvgre-packets"></a>NVGRE 和非 NVGRE 数据包


在混合转发环境中，有两种类型的进入和离开的 HYPER-V 可扩展交换机的数据包：NVGRE 数据包和非 NVGRE 数据包：

-   NVGRE 数据包将封装中指定的格式[NVGRE:使用通用路由封装网络虚拟化](http://ietfreport.isoc.org/idref/draft-sridharan-virtualization-nvgre/)Internet 草稿。 NVGRE 数据包由 HNV 组件的 HYPER-V 可扩展交换机的转发。
-   非 NVGRE 数据包是只是正常的网络数据包。 非 NVGRE 数据包都将由转发扩展转发 （或者，如果没有转发扩展，可扩展切换本身）。

## <a name="flow-of-nvgre-and-non-nvgre-packets-through-the-switch"></a>通过交换机的 NVGRE 和非 NVGRE 数据包的流


在入口数据路径中，捕获和筛选扩展之后、 之前转发扩展，如果数据包是 NVGRE 数据包，可扩展交换机设置**NativeForwardingRequired**标记中[ **NDIS\_交换机\_转发\_详细信息\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh598211)数据包的结构。 此结构包含在**NetBufferListInfo**的数据包的成员[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。

**请注意**   **NetBufferListInfo**的成员[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)通常称为数据包的"带外 (OOB) 数据。"

 

如果**NativeForwardingRequired**数据包的 OOB 数据中设置标志，该数据包是 NVGRE 数据包。 如果未设置，该数据包是非 NVGRE 数据包。

扩展均应使用[ **NET\_缓冲区\_列表\_开关\_转发\_详细**](https://msdn.microsoft.com/library/windows/hardware/hh598259)宏，以检查值**NativeForwardingRequired**标志。

NVGRE 和非 NVGRE 数据包将被视为，如下所示：

-   HYPER-V 可扩展交换机的 HNV 组件将转发 （即，确定的目标表） 所有 NVGRE 数据包
-   HNV 组件执行 NVGRE 封装并根据需要解封。
-   转发扩展转发所有非 NVGRE 数据包。
-   转发扩展不能转发 NVGRE 数据包，但它可以执行与筛选的扩展，包括添加或删除目标端口或者甚至丢弃数据包相同的筛选操作。
-   如果没有转发扩展，HYPER-V 可扩展交换机将转发的所有数据包。

有关详细信息，请参阅[数据包流通过可扩展的交换机数据路径](packet-flow-through-the-extensible-switch-data-path.md)。

## <a name="support-for-third-party-network-virtualization"></a>第三方网络虚拟化支持


一个**VirtualSubnetId**可以作为外部的虚拟子网的虚拟机网络适配器端口上配置。 添加了此功能，以启用转发扩展，以提供第三方网络虚拟化解决方案。 传入时，不会设置的 HYPER-V 可扩展交换机**NativeForwardingRequired**中的标志[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)这些数据包的结构。 然后，转发扩展可能修改数据包标头，根据需要，在转发期间。 要修改的数据包必须克隆和他们**ParentNetBufferList**指针设置为原始**NET\_缓冲区\_列表**。 (请参阅[克隆数据包流量](cloning-or-duplicating-packet-traffic.md)。)

## <a name="related-topics"></a>相关主题


[将可扩展交换机目标端口数据添加到数据包](adding-extensible-switch-destination-port-data-to-a-packet.md)

[克隆数据包流量](cloning-or-duplicating-packet-traffic.md)

[转发扩展](forwarding-extensions.md)

[通过可扩展交换机数据路径的数据包流](packet-flow-through-the-extensible-switch-data-path.md)

[**NET\_缓冲区\_列表\_交换机\_转发\_详细信息**](https://msdn.microsoft.com/library/windows/hardware/hh598259)

[**NDIS\_交换机\_转发\_详细信息\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh598211)

 

 






