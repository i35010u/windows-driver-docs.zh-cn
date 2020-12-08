---
title: 指示已从微型端口驱动程序收到数据
description: 指示已从微型端口驱动程序收到数据
keywords:
- 接收数据 WDK 网络
- NdisMIndicateReceiveNetBufferLists
- indicatings WDK NDIS 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e783006984e0237effbcfce773df307cf0d53768
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840645"
---
# <a name="indicating-received-data-from-a-miniport-driver"></a>指示已从微型端口驱动程序收到数据





下图说明了微型端口驱动程序接收指示。

![说明微型端口驱动程序接收指示的示意图](images/miniportreceive.png)

微型端口驱动程序调用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists) 函数，以指示从网络接收数据。 **NdisMIndicateReceiveNetBufferLists** 函数将指示的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的列表向上传递给过量的驱动程序。

如果微型端口驱动程序在 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)的 *ReceiveFlags* 参数中设置 **NDIS \_ 接收 \_ 标志 \_ 资源** 标志，则表明微型端口驱动程序必须立即重新获得 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的所有权。 在这种情况下，NDIS 不调用微型端口驱动程序的 [*MiniportReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists) 函数来返回 **网络 \_ 缓冲区 \_ 列表** 结构。 微型端口驱动程序在 **NdisMIndicateReceiveNetBufferLists** 返回后立即重新获得所有权。

如果微型端口驱动程序未在 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)的 *ReceiveFlags* 参数中设置 **ndis \_ 接收 \_ 标志 \_ 资源** 标志，ndis 会将指示的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构返回给微型端口驱动程序的 [*MiniportReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)函数。 在这种情况下，微型端口驱动程序让给指示的结构的所有权，直到 NDIS 将其返回给 *MiniportReturnNetBufferLists*。

 

