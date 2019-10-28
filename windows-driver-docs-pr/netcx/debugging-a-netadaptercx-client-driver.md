---
title: 调试 NetAdapterCx 客户端驱动程序
description: 调试 NetAdapterCx 客户端驱动程序
ms.assetid: EE8EA3DA-33E7-4EED-B991-38A21CAA699E
keywords:
- 调试 NetAdapterCx 客户端驱动程序，调试 NetAdapterCx 客户端驱动程序
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 64193125a6e51bc063d0edd85c1a86a635fbc5c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838283"
---
# <a name="debugging-a-netadaptercx-client-driver"></a>调试 NetAdapterCx 客户端驱动程序

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

你可以使用[Windows 驱动程序框架扩展（Wdfkd）](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)命令来调试你的客户端驱动程序。  此外， [！ ndiskd](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netadapter)将显示适配器的特定于网络的属性。

此外，还可以将 `!ndiskd.netrb` 调试程序扩展与[**NET_RING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringbuffer/ns-netringbuffer-_NET_RING)结构的地址一起使用，以在环形缓冲区中检查数据包和片段。  此命令提供额外的信息，例如环形缓冲区中的元素数，以及操作系统拥有的数据包数和客户端拥有的数据包数。

可以将以下！ ndiskd 命令与 NetAdapterCx 客户端驱动程序一起使用：

*  [ **!ndiskd.cxadapter**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-cxadapter)
    *  给定 GET-NETADAPTER 句柄，显示 GET-NETADAPTER 对象的相关信息。
*  [ **!ndiskd.netqueue**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netqueue)
    *  给定一个 NETTXQUEUE 或 NETRXQUEUE 句柄，显示有关数据路径队列的信息。
*  [ **!ndiskd.netrb**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netrb)
    *  显示[**NET_RING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netringbuffer/ns-netringbuffer-_NET_RING)信息。
*  [ **!ndiskd.netpacket**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netpacket)
    *  显示有关[**NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet)的信息。
*  [ **!ndiskd.netpacketfragment**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-ndiskd-netpacketfragment)
    *  显示有关[**NET_PACKET_FRAGMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet_fragment)的信息。
