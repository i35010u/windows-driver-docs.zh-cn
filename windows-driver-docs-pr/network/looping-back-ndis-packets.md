---
title: 环回 NDIS 数据包
description: 环回 NDIS 数据包
ms.assetid: 85967cd6-6945-46d1-8872-7b000689b6db
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a9de76262279f54f1fa8d203d97ce86f2f6798a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365864"
---
# <a name="looping-back-ndis-packets"></a>环回 NDIS 数据包





如果 NDIS\_NBL\_标志\_IS\_环回\_中的数据包标志**NblFlags**隶属[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)设置结构，该数据包是环回数据包。 协议驱动程序和筛选器驱动程序可以检查此标志，以确定数据包是否环回数据包。

NDIS 循环数据包，如果满足所有以下三个条件：

1.  媒体类型是基础的微型端口适配器**NdisMedium802\_3**或**NdisMedium802\_5**。

2.  满足以下三个条件之一：
    1.  协议绑定设置 NDIS\_数据包\_类型\_混杂设置[OID\_常规\_当前\_数据包\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569575)OID 来指定其数据包筛选器 (和 Windows 8 和更高版本，未设置 NDIS\_数据包\_类型\_否\_本地中相同的 OID) 和以下之一为 true:

        -   没有到微型端口适配器的多个绑定。
        -   连接到的微型端口适配器的筛选器模块和筛选器模块已注册接收处理程序。

    2.  协议绑定设置 NDIS\_数据包\_类型\_所有\_与本地设置[OID\_常规\_当前\_数据包\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569575) OID 来指定其数据包筛选器和以下任一为 true。
        -   没有到微型端口适配器的多个绑定。
        -   连接到的微型端口适配器的筛选器模块和筛选器模块已注册接收处理程序。

    3.  调用方设置 NDIS\_发送\_标志\_检查\_有关\_中的环回标志*SendFlags*参数[ **NdisSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564535)函数。

3.  数据包是由设置使用的数据包筛选器可接受[OID\_代\_当前\_数据包\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569575)微型端口适配器的 OID。 以下是一些示例：
    -   如果数据包是直接的数据包，数据包中的目标地址必须匹配微型端口适配器的 MAC 地址。
    -   如果数据包是多路广播的数据包，数据包筛选器必须具有 NDIS\_数据包\_类型\_所有\_多路广播的组或目标地址与某个多路广播地址匹配的微型端口适配器多播地址列表和数据包筛选器具有 NDIS\_数据包\_类型\_多播的组。
    -   如果数据包是广播的数据包，微型端口适配器的数据包筛选器必须具有 NDIS\_数据包\_类型\_广播集。
    -   微型端口适配器的数据包筛选器具有 NDIS\_数据包\_类型\_PROMISCUOUS 或 NDIS\_数据包\_类型\_所有\_本地组。

协议绑定接收环回数据包，如果以下任何一种情况：

1.  协议绑定是 NDIS 的数据包的原始发件人\_发送\_标志\_检查\_为\_设置环回。

2.  协议绑定不会设置 NDIS\_数据包\_类型\_否\_本地数据包筛选器中。

如果以下任何一种情况的协议绑定将不会收到环回数据包：

1.  协议绑定设置 NDIS\_数据包\_类型\_否\_数据包筛选器和它在本地不是数据包的原始发件人。

2.  协议绑定是原始的发件人但 NDIS\_发送\_标志\_检查\_有关\_中未设置环回*SendFlags* 的调用中的参数[**NdisSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff564535)函数。

下图显示了环回算法逻辑流。

![流程图，显示了环回算法逻辑流](images/loopback.png)

 

 





