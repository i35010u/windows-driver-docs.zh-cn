---
title: 调试 NetAdapterCx 客户端驱动程序
description: 调试 NetAdapterCx 客户端驱动程序
ms.assetid: EE8EA3DA-33E7-4EED-B991-38A21CAA699E
keywords:
- 调试 NetAdapterCx 客户端驱动程序，调试 NetAdapterCx 客户端驱动程序
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d51cadcdc719e668af8f983473685fa4dd456363
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323607"
---
# <a name="debugging-a-netadaptercx-client-driver"></a>调试 NetAdapterCx 客户端驱动程序

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

可以使用[Windows 驱动程序框架扩展 (Wdfkd.dll)](https://msdn.microsoft.com/library/windows/hardware/ff551876)命令来调试您的客户端驱动程序。  此外， [！ ndiskd.netadapter](https://msdn.microsoft.com/library/windows/hardware/mt799821)将显示您的适配器的特定于网络的属性。

此外，可以使用`!ndiskd.netrb`调试器扩展的地址[ **NET_RING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/ns-netringbuffer-_NET_RING)结构来检查数据包和环形缓冲区中的片段。  此命令将提供其他信息，如环形缓冲区，以及由操作系统拥有的数据包数量和归客户端的数据包数中的元素数。

可以使用以下 ！ ndiskd NetAdapterCx 客户端驱动程序的命令：

*  [**!ndiskd.cxadapter**](https://msdn.microsoft.com/library/windows/hardware/mt808786)
    *  给定的 NETADAPTER 句柄，显示有关 NETADAPTER 对象的信息。
*  [**!ndiskd.netqueue**](https://msdn.microsoft.com/library/windows/hardware/mt808789)
    *  给定 NETTXQUEUE 或 NETRXQUEUE 句柄，显示有关数据路径队列的信息。
*  [**!ndiskd.netrb**](https://msdn.microsoft.com/library/windows/hardware/mt808790)
    *  演示[ **NET_RING** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netringbuffer/ns-netringbuffer-_NET_RING)信息。
*  [**!ndiskd.netpacket**](https://msdn.microsoft.com/library/windows/hardware/mt808787)
    *  显示的信息是有关[ **NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet)。
*  [**!ndiskd.netpacketfragment**](https://msdn.microsoft.com/library/windows/hardware/mt808788)
    *  显示的信息是有关[ **NET_PACKET_FRAGMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet_fragment)。
