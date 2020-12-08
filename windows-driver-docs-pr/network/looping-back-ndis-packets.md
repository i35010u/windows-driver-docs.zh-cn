---
title: 环回 NDIS 数据包
description: 环回 NDIS 数据包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc141e097d20d4700bed048cc5f29c2b7203242e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833391"
---
# <a name="looping-back-ndis-packets"></a>环回 NDIS 数据包





如果 \_ \_ \_ \_ \_ 已设置 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的 **NblFlags** 成员中的 NDIS NBL 标志为环回数据包标志，则数据包是环回数据包。 协议驱动程序和筛选器驱动程序可以选中此标志来确定数据包是否为环回数据包。

如果满足以下三个条件，NDIS 会将数据包循环回来：

1.  基础微型端口适配器媒体类型为 **NdisMedium802 \_ 3** 或 **NdisMedium802 \_ 5**。

2.  满足以下三个条件之一：
    1.  协议绑定将 NDIS \_ 数据包 \_ 类型 \_ 混杂设置与 [OID 生成 \_ \_ 当前 \_ 数据包 \_ 筛选器](./oid-gen-current-packet-filter.md) oid 一起指定 (的数据包筛选器，对于 WINDOWS 8 及更高版本，未将 ndis \_ 数据包类型设置为 \_ \_ \_ 同一 OID 中的任何本地) 并且下列条件之一成立：

        -   有多个到小型端口适配器的绑定。
        -   有一个附加到微型端口适配器的筛选器模块和一个已注册接收处理程序的筛选器模块。

    2.  协议绑定将 NDIS \_ 数据包类型设置 \_ \_ \_ 为具有 [OID 生成 \_ \_ 当前 \_ 数据包 \_ 筛选器](./oid-gen-current-packet-filter.md) oid 的所有本地设置，以指定其数据包筛选器，并且下列任一条件为真。
        -   有多个到小型端口适配器的绑定。
        -   有一个附加到微型端口适配器的筛选器模块和一个已注册接收处理程序的筛选器模块。

    3.  调用方设置 \_ \_ \_ \_ \_ [**NdisSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)函数的 *SendFlags* 参数中的 "NDIS 发送标志检查" 标记。

3.  数据包是可接受的，该数据包筛选器集具有用于微型端口适配器的 [oid 生成 \_ \_ 当前 \_ 数据包 \_ 筛选器](./oid-gen-current-packet-filter.md) oid。 下面是一些示例：
    -   如果数据包是直接数据包，则数据包中的目标地址必须与微型端口适配器的 MAC 地址匹配。
    -   如果数据包是多路广播数据包，则数据包筛选器必须具有 NDIS \_ 数据包 \_ 类型， \_ 所有 \_ 多播集或目标地址与微型端口适配器的多播地址列表中的一个多播地址或目标地址匹配，并且数据包筛选器具有 NDIS \_ 数据包 \_ 类型 \_ 多播集。
    -   如果数据包是广播数据包，则微型端口适配器的数据包筛选器必须具有 NDIS \_ 数据包 \_ 类型 \_ 广播集。
    -   微型端口适配器的数据包筛选器具有 NDIS \_ 数据包 \_ 类型 \_ 混杂或 ndis \_ 数据包 \_ 类型 \_ ALL \_ 本地集。

如果满足以下任一条件，则协议绑定会接收环回数据包：

1.  协议绑定是数据包的原始发送方，并设置了 \_ 环回的 NDIS 发送 \_ 标志 \_ 检查 \_ \_ 。

2.  协议绑定未 \_ \_ \_ \_ 在数据包筛选器中设置 NDIS 数据包类型 NO LOCAL。

如果满足以下任一条件，则协议绑定不会接收环回数据包：

1.  协议绑定在 \_ \_ \_ 数据包筛选器中设置 NDIS 数据包类型 NO \_ LOCAL，而不是数据包的原始发件人。

2.  协议绑定是原始发送方，但对 \_ \_ \_ \_ \_ [**NdisSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissendnetbufferlists)函数的调用中未在 *SendFlags* 参数中设置环回的 NDIS 发送标志检查。

下图显示了环回算法的逻辑流。

![说明环回算法逻辑流的流程图](images/loopback.png)

 

