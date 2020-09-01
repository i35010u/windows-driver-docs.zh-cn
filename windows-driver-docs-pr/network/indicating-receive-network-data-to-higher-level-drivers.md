---
title: 指示将网络数据接收到更高级别的驱动程序
description: 指示将网络数据接收到更高级别的驱动程序
ms.assetid: 27272427-86bc-4fd3-bd2f-12d94273fcd4
keywords:
- 中间驱动程序 WDK 网络，接收操作
- NDIS 中间驱动程序 WDK，接收操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4475315ef4ca2ac6dea6969e9f1b1c05fc75dbf1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212427"
---
# <a name="indicating-receive-network-data-to-higher-level-drivers"></a>指示将网络数据接收到更高级别的驱动程序





无连接中间驱动程序指示通过调用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists) 函数将网络数据接收到下一个更高的驱动程序。 面向连接的中间驱动程序指示通过调用 [**NdisMCoIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists) 函数将网络数据接收到下一个更高的驱动程序。

在指示接收网络数据之前，驱动程序将处理数据，可能会将其转换为较高级别的驱动程序所需的格式，并根据需要将相关数据复制到与中间驱动程序分配的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构关联的 MDLs 中。

 

