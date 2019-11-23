---
title: 在 CoNDIS 驱动程序中接收 NET_BUFFER 结构
description: 在 CoNDIS 驱动程序中接收 NET_BUFFER 结构
ms.assetid: b3bbd3ef-9206-4edc-8f7a-4ce896d77150
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2558990f10e584eeb8af069788a45bd423157846
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844845"
---
# <a name="receiving-net_buffer-structures-in-condis-drivers"></a>在 CoNDIS 驱动程序中接收 NET\_缓冲区结构





下图说明了一个基本 CoNDIS 接收操作，该操作涉及一个协议驱动程序、NDIS 和一个微型端口驱动程序。

![说明基本 condis 接收操作（涉及协议驱动程序、ndis 和微型端口驱动程序）的示意图](images/netbuffercoreceive.png)

如上图所示，微型端口驱动程序调用[**NdisMCoIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)函数，以指示对过量驱动程序的[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构。 在大多数微型端口驱动程序中，每个网络\_缓冲结构都附加到单独的[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构，因此协议驱动程序可以创建一组原始的 NET\_缓冲区\_列表结构，并将其转发到不同的客户端。 但是，附加到网络\_缓冲区\_列表的净\_缓冲区的数量取决于驱动程序。

当微型端口驱动程序将所有 NET\_缓冲区链接\_列表结构后，微型端口驱动程序会将该列表中第一个网络\_\_缓冲区的指针传递到**NdisMCoIndicateReceiveNetBufferLists**函数。 NDIS 检查 NET\_缓冲区\_列表结构并调用与指定虚拟连接（VC）关联的协议驱动程序的[**ProtocolCoReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_receive_net_buffer_lists)函数。 NDIS 传递列表的一个子集，该子集只包含与每个协议驱动程序的正确绑定关联的 NET\_缓冲区\_列表结构。

如果在*CoReceiveFlags*参数中为协议驱动程序的*ProtocolCoReceiveNetBufferLists*函数设置了 NDIS\_接收\_标志\_状态\_资源标志，则在*ProtocolCoReceiveNetBufferLists*返回后，ndis 会立即重新获得[**网络\_缓冲区的所有权\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构。

如果 NDIS\_接收\_标志\_状态\_资源标志未在协议驱动程序的[**ProtocolCoReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_receive_net_buffer_lists)函数的*CoReceiveFlags*参数中设置，则协议驱动程序可保留 NET\_缓存\_列表结构的所有权。 在这种情况下，协议驱动程序必须通过调用[**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)函数来返回 NET\_缓冲区\_列表结构。

如果微型端口驱动程序在接收资源上运行较少，则可以在[**NdisMCoIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)函数的*CoReceiveFlags*参数中将 NDIS\_接收\_标志\_状态\_资源标志。 在这种情况下，只要**NdisMCoIndicateReceiveNetBufferLists**返回，驱动程序就可以回收所有指定的[**net\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构和嵌入的[**net\_缓冲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的所有权。 如果微型端口驱动程序使用 NDIS\_接收\_标志\_资源标志来指示 NET\_缓冲区结构，则协议驱动程序必须复制数据，因此应避免使用 NDIS\_以这种方式\_资源接收\_标志。 微型端口驱动程序应检测其接收资源不足的情况，并应完成避免此情况所需的任何步骤。

在协议驱动程序调用**NdisReturnNetBufferLists**后，NDIS 调用微型端口驱动程序的[*MiniportReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)函数。

**请注意**  如果微型端口驱动程序指示具有给定状态的[**网络\_缓冲器\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构，则不需要使用 NDIS 向状态相同的过量驱动程序指示网络\_缓冲区\_列表结构。 例如，NDIS 可以使用 NDIS\_接收\_标志\_资源标志来复制网络\_缓冲区\_列表结构，并指示清除了此标志的过量驱动程序的副本。

 

NDIS 可以按任意顺序和任意组合将 NET\_缓冲区\_列表结构返回到小型端口驱动程序。 也就是说，通过调用[*MiniportReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists) ，NDIS 返回到微型端口驱动程序的 NET\_缓冲区\_列表结构的链接列表可以具有 NET\_BUFFER\_列表结构，从以前对[**NdisMCoIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)的调用不同。

微型端口驱动程序必须将[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中的**SourceHandle**成员设置为与**NdisMCoIndicateReceiveNetBufferLists**的*NdisVcHandle*参数相同的值。 因此，NDIS 可以将 NET\_BUFFER\_列表结构返回到正确的微型端口驱动程序。

中间驱动程序还将 NET\_BUFFER\_列表结构中的**SourceHandle**成员设置为*NdisVcHandle*值。 如果中间驱动程序转发接收指示，则驱动程序必须保存基础驱动程序在写入**SourceHandle**成员之前提供的**SourceHandle**值。 当 NDIS 向中间驱动程序返回已转发的 NET\_缓冲区\_列表结构时，中间驱动程序必须还原它保存的**SourceHandle** 。

 

 





