---
title: 指示将网络数据接收到更高级别的驱动程序
description: 指示将网络数据接收到更高级别的驱动程序
keywords:
- 中间驱动程序 WDK 网络，接收操作
- NDIS 中间驱动程序 WDK，接收操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76083fcaa73a18d2b0bf6e2f3b8acef5322a3ee1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832241"
---
# <a name="indicating-receive-network-data-to-higher-level-drivers"></a>指示将网络数据接收到更高级别的驱动程序





无连接中间驱动程序指示通过调用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists) 函数将网络数据接收到下一个更高的驱动程序。 面向连接的中间驱动程序指示通过调用 [**NdisMCoIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists) 函数将网络数据接收到下一个更高的驱动程序。

在指示接收网络数据之前，驱动程序将处理数据，可能会将其转换为较高级别的驱动程序所需的格式，并根据需要将相关数据复制到与中间驱动程序分配的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构关联的 MDLs 中。

 

