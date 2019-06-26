---
title: 指示将网络数据接收到更高级别的驱动程序
description: 指示将网络数据接收到更高级别的驱动程序
ms.assetid: 27272427-86bc-4fd3-bd2f-12d94273fcd4
keywords:
- 中间驱动程序 WDK 网络，接收操作
- NDIS 驱动程序 WDK 的中间，接收操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3c8b81ecd6cd88967ac5e27101ddf148aa53c7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380917"
---
# <a name="indicating-receive-network-data-to-higher-level-drivers"></a>指示将网络数据接收到更高级别的驱动程序





无连接的中间驱动程序指示接收到下一个更高版本的驱动程序的网络数据，方法是调用[ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数。 面向连接的中间驱动程序指示接收到下一个更高版本的驱动程序的网络数据，方法是调用[ **NdisMCoIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)函数。

之前，该值指示接收网络数据，可能将其转换为格式的数据所需的更高级别的驱动程序的驱动程序进程和必要情况下，将相关的数据复制到 MDLs 所带来的中间驱动程序分配[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构。

 

 





