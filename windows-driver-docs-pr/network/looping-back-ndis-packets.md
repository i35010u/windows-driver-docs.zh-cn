---
title: 环回 NDIS 数据包
description: 环回 NDIS 数据包
ms.assetid: 85967cd6-6945-46d1-8872-7b000689b6db
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60ea3a48e62577669508551cd1bfc92a65e842b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844142"
---
# <a name="looping-back-ndis-packets"></a>环回 NDIS 数据包





如果 NDIS\_NBL\_标志\_为[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)的**NblFlags**成员中\_环回\_数据包标志，则数据包是环回数据包。 协议驱动程序和筛选器驱动程序可以选中此标志来确定数据包是否为环回数据包。

如果满足以下三个条件，NDIS 会将数据包循环回来：

1.  基础微型端口适配器媒体类型为**NdisMedium802\_3**或**NdisMedium802\_5**。

2.  满足以下三个条件之一：
    1.  协议绑定将 NDIS\_数据包\_类型\_混杂设置与[OID\_GEN\_当前\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)oid 来指定其数据包筛选器（对于 Windows 8 及更高版本，则设置为，未将 NDIS\_数据包\_类型\_在同一 OID 中没有\_LOCAL），并且以下条件之一成立：

        -   有多个到小型端口适配器的绑定。
        -   有一个附加到微型端口适配器的筛选器模块和一个已注册接收处理程序的筛选器模块。

    2.  协议绑定将 NDIS\_数据包\_类型\_所有\_本地设置，并使用[OID\_\_当前\_包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)oid 来指定其数据包筛选器，并且以下条件之一为 true。
        -   有多个到小型端口适配器的绑定。
        -   有一个附加到微型端口适配器的筛选器模块和一个已注册接收处理程序的筛选器模块。

    3.  调用方将 NDIS\_发送\_标志\_\_检查[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)函数的*SendFlags*参数中\_环回标志。

3.  如果数据包筛选器集使用[OID\_GEN\_当前\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)OID，则可接受此数据包，这是微型端口适配器的筛选器 oid。 下面是一些示例：
    -   如果数据包是直接数据包，则数据包中的目标地址必须与微型端口适配器的 MAC 地址匹配。
    -   如果数据包是多路广播数据包，则数据包筛选器必须具有 NDIS\_数据包\_类型\_所有\_多播集或目标地址匹配微型端口适配器的多播地址列表中的某个多播地址和数据包筛选器具有 NDIS\_数据包\_类型\_多播集。
    -   如果数据包是广播数据包，则微型端口适配器的数据包筛选器必须具有 NDIS\_数据包\_类型\_广播集。
    -   微型端口适配器的数据包筛选器具有 NDIS\_数据包\_类型\_混合或 NDIS\_包\_类型\_所有\_本地集。

如果满足以下任一条件，则协议绑定会接收环回数据包：

1.  协议绑定是数据包的原始发送方，NDIS\_发送\_标志\_\_检查是否设置了\_环回。

2.  协议绑定未将 NDIS\_数据包\_类型\_在数据包筛选器中没有\_本地。

如果满足以下任一条件，则协议绑定不会接收环回数据包：

1.  协议绑定会将 NDIS\_数据包\_类型\_在数据包筛选器中不\_本地，并且它不是数据包的原始发送方。

2.  协议绑定是原始发送方，但 NDIS\_发送\_标志\_\_检查在调用[**NdisSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)函数时，未在*SendFlags*参数中设置\_环回。

下图显示了环回算法的逻辑流。

![说明环回算法逻辑流的流程图](images/loopback.png)

 

 





