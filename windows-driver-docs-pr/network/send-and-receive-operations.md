---
title: 发送和接收操作
description: 发送和接收操作
ms.assetid: 216bfed2-92f8-4480-95fc-9909d7c1f533
keywords:
- 网络数据 WDK，发送
- 网络数据 WDK，接收
- 数据 WDK 连接网络、 发送
- WDK 数据网络、 接收
- 发送数据 WDK 网络
- 接收数据 WDK 网络
- NET_BUFFER_LIST
- 多个 NET_BUFFER_LIST 结构 WDK networki
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2652409e479fd2e1823754011352af8cbd9ef049
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568735"
---
# <a name="send-and-receive-operations"></a>发送和接收操作





在单个函数调用，NDIS 6.0 驱动程序可以发送多个[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构具有多个[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)每个网络上的结构\_缓冲区\_列表结构。 此外，NDIS 驱动程序可以指示已完成的发送操作的多个 NET\_缓冲区\_具有多个网络的列表结构\_网上缓冲区结构\_缓冲区\_列表结构。

在接收路径微型端口驱动程序可以使用一系列 NET\_缓冲区\_列表结构，以指示接收。 每个 NET\_缓冲区\_为由微型端口驱动程序的列表包含一个 NET\_缓冲区结构。 但是，本机 802.11 驱动程序可以具有多个 NET\_缓冲区结构。 因为不同的协议绑定可以处理每个 NET\_缓冲区\_列表结构 NDIS 可以返回每个 NET\_缓冲区\_单独列出微型端口驱动程序的结构。

若要支持 NDIS 5。*x*和早期版本的驱动程序，NDIS 提供之间创建转换层[ **NDIS\_数据包**](https://msdn.microsoft.com/library/windows/hardware/ff557086)-基于和 NET\_基于缓冲区的接口。 NDIS 执行必要的转换之间[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构和 NDIS\_数据包结构。 若要避免由于转换的性能下降，必须为 NDIS 驱动程序更新为使用 NET\_缓冲结构，并且应该支持多个[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)所有的数据路径中的结构。

本部分包括以下主题：

[发送的网络数据](sending-network-data.md)

[取消发送操作](canceling-a-send-operation.md)

[接收网络数据](receiving-network-data.md)

[循环后的 NDIS 数据包](looping-back-ndis-packets.md)

 

 





