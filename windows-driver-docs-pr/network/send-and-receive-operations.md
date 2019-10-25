---
title: 发送和接收操作
description: 发送和接收操作
ms.assetid: 216bfed2-92f8-4480-95fc-9909d7c1f533
keywords:
- 网络数据 WDK，发送
- 网络数据 WDK，接收
- 数据 WDK 网络，发送
- 数据 WDK 网络，接收
- 发送数据 WDK 网络
- 接收数据 WDK 网络
- NET_BUFFER_LIST
- 多个 NET_BUFFER_LIST 结构 WDK networki
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02f562ef824766b0cf881c2fca4e399c1fba478d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841985"
---
# <a name="send-and-receive-operations"></a>发送和接收操作





在单个函数调用中，NDIS 6.0 驱动程序可以将多个 net [ **\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构发送到每个网络\_缓冲区\_列表结构的多个 NET [ **\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构。 此外，NDIS 驱动程序还可以针对多个 net\_缓冲区\_列表结构\_\_中的多个 net\_缓冲结构来指示已完成的发送操作。

在接收路径中，微型端口驱动程序可以使用网络\_缓冲区的列表\_列表结构来指示接收。 微型端口驱动程序指示的每个网络\_缓冲区\_列表包含一个网络\_缓冲区结构。 但是，本机802.11 驱动程序可以有多个 NET\_缓冲区结构。 由于不同的协议绑定可以处理每个网络\_缓冲区\_列表结构，因此 NDIS 可以将每个 NET\_缓冲区\_列表结构单独返回到微型端口驱动程序。

支持 NDIS 5。*x*及更早版本的驱动程序，Ndis 在[**NDIS\_基于数据包**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))和网络\_基于缓冲区的接口之间提供转换层。 NDIS 在[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构与 NDIS\_数据包结构之间执行必要的转换。 为了避免由于转换而导致性能下降，必须更新 NDIS 驱动程序以使用 NET\_缓冲区结构，并且应支持所有数据路径中的多个[**net\_缓冲器\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。

本部分包括下列主题：

[发送网络数据](sending-network-data.md)

[取消发送操作](canceling-a-send-operation.md)

[接收网络数据](receiving-network-data.md)

[循环回 NDIS 数据包](looping-back-ndis-packets.md)

 

 





