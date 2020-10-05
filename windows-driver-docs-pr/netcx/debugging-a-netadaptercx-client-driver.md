---
title: 调试 NetAdapterCx 客户端驱动程序
description: 调试 NetAdapterCx 客户端驱动程序
ms.assetid: EE8EA3DA-33E7-4EED-B991-38A21CAA699E
keywords:
- 调试 NetAdapterCx 客户端驱动程序，调试 NetAdapterCx 客户端驱动程序
ms.date: 06/17/2020
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 3533e805c79801ac33364cddd0ccebdf59d25745
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733250"
---
# <a name="debugging-a-netadaptercx-client-driver"></a>调试 NetAdapterCx 客户端驱动程序

你可以使用 [Windows 驱动程序框架扩展 ( # A0) ](../debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-.md) 命令调试你的客户端驱动程序。  此外， [！ ndiskd](../debugger/-ndiskd-netadapter.md) 将显示适配器的特定于网络的属性。

此外，还可以将 `!ndiskd.netrb` 调试程序扩展与 [**NET_RING**](/windows-hardware/drivers/ddi/ring/ns-ring-_net_ring) 结构的地址一起使用，以在环形缓冲区中检查数据包和片段。  此命令提供额外的信息，例如环形缓冲区中的元素数，以及操作系统拥有的数据包数和客户端拥有的数据包数。

可以将以下！ ndiskd 命令与 NetAdapterCx 客户端驱动程序一起使用：

*  [**!ndiskd.cxadapter**](../debugger/-ndiskd-cxadapter.md)
    *  给定 GET-NETADAPTER 句柄，显示 GET-NETADAPTER 对象的相关信息。
*  [**!ndiskd.netqueue**](../debugger/-ndiskd-netqueue.md)
    *  给定一个 NETTXQUEUE 或 NETRXQUEUE 句柄，显示有关数据路径队列的信息。
*  [**!ndiskd.netrb**](../debugger/-ndiskd-netrb.md)
    *  显示 [**NET_RING**](/windows-hardware/drivers/ddi/ring/ns-ring-_net_ring) 信息。
*  [**!ndiskd.netpacket**](../debugger/-ndiskd-netpacket.md)
    *  显示有关 [**NET_PACKET**](/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet)的信息。
*  [**!ndiskd.netfragment**](../debugger/-ndiskd-netfragment.md)
    *  显示有关 [**NET_PACKET_FRAGMENT**](/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet_fragment)的信息。