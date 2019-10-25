---
title: 指示将网络数据接收到更高级别的驱动程序
description: 指示将网络数据接收到更高级别的驱动程序
ms.assetid: 27272427-86bc-4fd3-bd2f-12d94273fcd4
keywords:
- 中间驱动程序 WDK 网络，接收操作
- NDIS 中间驱动程序 WDK，接收操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82df5e75b5b8880d7798b337e3b4418c5df96fa8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824663"
---
# <a name="indicating-receive-network-data-to-higher-level-drivers"></a>指示将网络数据接收到更高级别的驱动程序





无连接中间驱动程序指示通过调用[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数将网络数据接收到下一个更高的驱动程序。 面向连接的中间驱动程序指示通过调用[**NdisMCoIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)函数将网络数据接收到下一个更高的驱动程序。

在指示接收网络数据之前，驱动程序将处理数据，可能会将其转换为较高级别的驱动程序所需的格式，并根据需要将相关数据复制到与中间驱动程序分配的网络关联的 MDLs 中。 [ **\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构。

 

 





