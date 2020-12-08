---
title: 网络驱动程序中的数据包结构
description: 网络驱动程序中的数据包结构
keywords:
- 数据包 WDK 网络
- 网络驱动程序 WDK，数据包
- 网络数据 WDK
- 数据 WDK 网络
- 网络数据包结构 WDK
- 网络数据缓冲区 WDK
- 数据缓冲区 WDK 网络
- 网络数据 WDK，结构
- 数据 WDK 网络，结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6b8dfaaa1fe05fa7698e049653a3828489654ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812851"
---
# <a name="packet-structures-in-network-drivers"></a>网络驱动程序中的数据包结构





在 NDIS 6.0 和更高版本中，较高层的驱动程序分配网络 [**\_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 和 [**网络 \_ 缓冲区列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构来保存网络数据包信息，并将这些结构发送到下一个较低的 NDIS 驱动程序，以便可以在网络上发送数据。 较低级别的驱动程序分配网络 \_ 缓冲区和网络 \_ 缓冲区 \_ 列表结构来保存接收的数据，并将这些结构传递到相关的更高层驱动程序。 有时，较高层的驱动程序会分配结构，并将其传递到较低的层驱动程序，请求使用较低层的驱动程序将接收的数据复制到提供的缓冲区中。 NDIS 提供了用于分配和操作子结构的函数，这些函数构成网络 \_ 缓冲区和网络 \_ 缓冲区 \_ 列表结构。

有关 NDIS 驱动程序中网络数据缓冲区结构的详细信息，请参阅 [NET \_ BUFFER](net-buffer-architecture.md)structure。

 

