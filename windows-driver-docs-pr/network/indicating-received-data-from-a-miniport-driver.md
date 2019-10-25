---
title: 指示已从微型端口驱动程序收到数据
description: 指示已从微型端口驱动程序收到数据
ms.assetid: da5d31e9-5212-4c6c-bac2-81432a46c303
keywords:
- 接收数据 WDK 网络
- NdisMIndicateReceiveNetBufferLists
- indicatings WDK NDIS 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5684ae3e1d6ecd0d4a454e8f77536308ad7306f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824626"
---
# <a name="indicating-received-data-from-a-miniport-driver"></a>指示已从微型端口驱动程序收到数据





下图说明了微型端口驱动程序接收指示。

![说明微型端口驱动程序接收指示的示意图](images/miniportreceive.png)

微型端口驱动程序调用[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数，以指示从网络接收数据。 **NdisMIndicateReceiveNetBufferLists**函数将所指示的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的列表传递给过量的驱动程序。

如果微型端口驱动程序设置 NDIS\_在[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)的*RECEIVEFLAGS*参数中**接收\_标志\_资源**标志，则表明微型端口驱动程序必须重新获得[**NET\_缓冲区会立即\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。 在这种情况下，NDIS 不会调用微型端口驱动程序的[*MiniportReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)函数来返回**NET\_缓冲区\_列表**结构。 微型端口驱动程序在**NdisMIndicateReceiveNetBufferLists**返回后立即重新获得所有权。

如果微型端口驱动程序未在[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)的*ReceiveFlags*参数中将**ndis\_接收\_标志\_资源**标志，ndis 将返回指定的[**网络\_缓冲区\_列出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)微型端口驱动程序的[*MiniportReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)函数的结构。 在这种情况下，微型端口驱动程序让给指示的结构的所有权，直到 NDIS 将其返回给*MiniportReturnNetBufferLists*。

 

 





