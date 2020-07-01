---
title: 调试 NetAdapterCx 客户端驱动程序
description: 调试 NetAdapterCx 客户端驱动程序
ms.assetid: EE8EA3DA-33E7-4EED-B991-38A21CAA699E
keywords:
- 调试 NetAdapterCx 客户端驱动程序，调试 NetAdapterCx 客户端驱动程序
ms.date: 06/17/2020
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 769698e26296355645940e52c5842105432a2e83
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593961"
---
# <a name="debugging-a-netadaptercx-client-driver"></a>调试 NetAdapterCx 客户端驱动程序

你可以使用[Windows 驱动程序框架扩展（Wdfkd.dll）](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)命令来调试你的客户端驱动程序。  此外， [！ ndiskd](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netadapter)将显示适配器的特定于网络的属性。

此外，还可以将 `!ndiskd.netrb` 调试程序扩展与[**NET_RING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringbuffer/ns-netringbuffer-_NET_RING)结构的地址一起使用，以在环形缓冲区中检查数据包和片段。  此命令提供额外的信息，例如环形缓冲区中的元素数，以及操作系统拥有的数据包数和客户端拥有的数据包数。

可以将以下！ ndiskd 命令与 NetAdapterCx 客户端驱动程序一起使用：

*  [**!ndiskd.cxadapter**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-cxadapter)
    *  给定 GET-NETADAPTER 句柄，显示 GET-NETADAPTER 对象的相关信息。
*  [**!ndiskd.netqueue**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netqueue)
    *  给定一个 NETTXQUEUE 或 NETRXQUEUE 句柄，显示有关数据路径队列的信息。
*  [**!ndiskd.netrb**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netrb)
    *  显示[**NET_RING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringbuffer/ns-netringbuffer-_NET_RING)信息。
*  [**!ndiskd.netpacket**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netpacket)
    *  显示有关[**NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet)的信息。
*  [**!ndiskd.netfragment**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netfragment)
    *  显示有关[**NET_PACKET_FRAGMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet_fragment)的信息。
