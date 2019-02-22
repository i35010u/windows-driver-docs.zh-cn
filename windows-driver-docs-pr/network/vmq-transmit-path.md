---
title: VMQ 传输路径
description: VMQ 传输路径
ms.assetid: a34f0708-e477-4acc-b854-f00f752be423
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdd173f2f25e2ef72373f1cc16fbbbf3e5237f2e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541185"
---
# <a name="vmq-transmit-path"></a>VMQ 传输路径





对于传输请求，使用过量的驱动程序[ **NET\_缓冲区\_列表\_接收\_队列\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff568407)宏设置队列中具有的传出数据的传出队列的标识符**NetBufferListFilteringInfo** OOB 信息。 **NetBufferListFilteringInfo**中指定的信息[ **NDIS\_NET\_缓冲区\_列表\_筛选\_信息** ](https://msdn.microsoft.com/library/windows/hardware/ff566567)结构。

NDIS 驱动程序可以使用[ **NET\_缓冲区\_列表\_接收\_队列\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff568407)宏来设置或获取队列的标识符[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 如果队列组包含多个虚拟机队列，传输数据包的队列标识符可能设置为任何组中的 VM 队列队列标识符。

协议驱动程序设置 NDIS\_发送\_标志\_单个\_位上的队列*SendFlags*参数[ **NdisSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff564535)函数来指示所有传输 NET\_缓冲区\_列表结构的调用中是相同的传输队列。

微型端口驱动程序设置 NDIS\_发送\_完成\_标志\_单个\_位上的队列*SendCompleteFlags*参数[ **NdisMSendNetBufferListsComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563668)函数来指示所有 NET\_缓冲区\_在相同的传输队列发送调用中的列表。

有关筛选器测试的详细信息，请参阅[VMQ 筛选器操作](vmq-filter-operations.md)。

**请注意**  时 VMQ 删除 （例如，在虚拟机实时迁移），则可以为微型端口驱动程序以接收包含一个无效的 NBL **QueueId**值。 如果发生这种情况，应忽略无效的队列 ID 微型端口并将其改为使用 0 （默认队列）。 **QueueId**中找到**NetBufferListFilteringInfo** NBL 部分的 OOB 数据，并通过使用检索[ **NET\_缓冲区\_列表\_接收\_队列\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff568407)宏。

 

 

 





