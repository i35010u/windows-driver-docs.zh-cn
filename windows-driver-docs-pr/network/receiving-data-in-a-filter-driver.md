---
title: 在筛选器驱动程序中接收数据
description: 在筛选器驱动程序中接收数据
ms.assetid: 4f6d44e9-c351-452d-aadf-505e6bb30fc2
keywords:
- 接收数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82db7e92f1b62eb16ec8471f9f7e205cc497b460
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373330"
---
# <a name="receiving-data-in-a-filter-driver"></a>在筛选器驱动程序中接收数据





筛选器驱动程序可以启动接收指示或筛选器从基础驱动程序接收的指示。 当微型端口驱动程序调用[ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数，NDIS 提交指定[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构中的驱动程序堆栈的最低基础筛选器模块。

### <a name="receive-indications-initiated-by-a-filter-driver"></a>接收指示由筛选器驱动程序启动

下图说明了由筛选器驱动程序启动的接收指示。

![说明由筛选器驱动程序启动的接收指示的关系图](images/filterreceive.png)

筛选驱动程序调用[ **NdisFIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)函数来指示接收到的数据。 **NdisFIndicateReceiveNetBufferLists**函数将指示的列表传递[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构在堆栈中向上到基础驱动程序。 筛选器驱动程序会在初始化期间创建的池将分配结构。

如果筛选器驱动程序设置**NDIS\_接收\_标志\_资源**标志中*ReceiveFlags*参数[ **NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)，这表示筛选器驱动程序必须重新获得的所有权[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)立即结构。 在这种情况下，NDIS 不会调用筛选器驱动程序[ *FilterReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_return_net_buffer_lists)函数以返回**NET\_缓冲区\_列表**结构。 筛选器驱动程序重新获得所有权后立即**NdisFIndicateReceiveNetBufferLists**返回。

如果未设置筛选器驱动程序不会**NDIS\_接收\_标志\_资源**标志中*ReceiveFlags*参数[ **NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)，返回所指示的 NDIS [ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)到结构筛选器驱动程序[ *FilterReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_return_net_buffer_lists)函数。 在这种情况下，筛选器驱动程序将放弃所指示的结构的所有权，直到 NDIS 返回到*FilterReturnNetBufferLists*。

**请注意**  应跟踪的筛选器驱动程序收到指示它启动，并确保它不会调用[ **NdisFReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreturnnetbufferlists)函数时接收操作已完成。

 

### <a name="filtering-receive-indications"></a>筛选接收指示

下图说明了筛选会收到指示由基础驱动程序启动。

![说明已筛选的关系图会收到指示由基础驱动程序启动](images/receivefilter.png)

NDIS 筛选器驱动程序将调用[ *FilterReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)函数来处理接收来自基础驱动程序的迹象。 NDIS 调用*FilterReceiveNetBufferLists*基础驱动程序调用接收指示函数后 (例如， [ **NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists))若要指示接收的网络数据或环回数据。

如果**NDIS\_接收\_标志\_资源**标志中*ReceiveFlags*参数[ *FilterReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)未设置，筛选器驱动程序保留的所有权[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构之前它将调用[ **NdisFReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreturnnetbufferlists)函数。

如果**NDIS\_接收\_标志\_资源**标志中*ReceiveFlags*设置参数，则筛选器驱动程序不能保留[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构和关联基础驱动程序分配的资源。 此标志可以指示不足基础驱动程序获得资源。 [ *FilterReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)函数应尽可能快地返回。

**请注意**  如果**NDIS\_接收\_标志\_资源**设置标志，则筛选器驱动程序必须保留原来的一组[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)链接列表中的结构。 例如，设置此标志，该驱动程序可能会处理结构并指示它们其中一个在堆栈中向上一次，但该函数返回之前，它必须还原原始链接的列表。

 

筛选器驱动程序，该值指示基础驱动程序的数据之前可以执行筛选器上接收到的数据的操作。 每个缓冲区提交到其[ *FilterReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)函数筛选器驱动程序可以执行以下操作：

-   将其传递到下一步基础驱动程序通过调用[ **NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)。 该驱动程序可以修改缓冲区的内容。 NDIS 保证上下文空间的可用性 (请参阅[NET\_缓冲区\_列表\_上下文结构](net-buffer-list-context-structure.md))。

    筛选器驱动程序可以更改状态的 NDIS 传递给[ *FilterReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists) ，或只需将传递到[ **NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatereceivenetbufferlists).

    **请注意**  筛选器驱动程序可以将传递的缓冲区[ **NdisFIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)即使 NDIS 设置**NDIS\_接收\_标志\_资源**中的标志*ReceiveFlags*参数[ *FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)。 在这种情况下，筛选器驱动程序不能返回从*FilterReceiveNetBufferLists*直到它重新获得所有权的缓冲区。

     

-   放弃缓冲区。 如果清除 NDIS **NDIS\_接收\_标志\_资源**标志中*ReceiveFlags*参数[ *FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)，调用[ **NdisFReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreturnnetbufferlists)放弃缓冲区的函数。 如果设置 NDIS **NDIS\_接收\_标志\_资源**标志中*ReceiveFlags*参数*FilterReceiveNetBufferLists*、 不执行任何操作并返回从*FilterReceiveNetBufferLists*放弃缓冲区。

-   排入队列供以后处理的本地数据结构中的缓冲区。 如果设置 NDIS **NDIS\_接收\_标志\_资源**标志中*ReceiveFlags*参数[ *FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)，筛选器驱动程序必须返回从之前创建副本*FilterReceiveNetBufferLists*。

-   将缓冲区复制并且源自与复制的接收指示。 接收指示是类似的筛选器驱动程序启动接收指示。 在这种情况下，该驱动程序必须返回到基础驱动程序的原始缓冲区。

[ **NdisFIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)函数将指示的列表传递[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构最多到过量驱动程序的驱动程序堆栈。 接收操作同样继续筛选器驱动程序启动接收操作。

如果基础驱动程序保留的缓冲区的所有权，调用 NDIS [ *FilterReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_return_net_buffer_lists)筛选器模块的函数。 在其*FilterReturnNetBufferLists*函数，筛选器驱动程序将撤消其上接收指示路径的缓冲区执行的操作。

在最低层筛选器模块指示它通过一个缓冲区，NDIS 微型端口驱动程序返回的缓冲区。 如果清除 NDIS **NDIS\_接收\_标志\_资源**标志中*ReceiveFlags*参数[ *FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)，筛选器驱动程序调用[ **NdisFReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreturnnetbufferlists)返回缓冲区。 如果设置 NDIS **NDIS\_接收\_标志\_资源**标志中*ReceiveFlags*参数*FilterReceiveNetBufferLists*，使其返回从*FilterReceiveNetBufferLists*返回的缓冲区。

 

 





