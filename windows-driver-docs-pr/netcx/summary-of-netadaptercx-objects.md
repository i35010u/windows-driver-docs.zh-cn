---
title: NetAdapterCx 对象的摘要
description: NetAdapterCx 对象的摘要
ms.assetid: 1635C737-42C6-4957-A3E0-1184A5545441
keywords:
- 摘要 NetAdapterCx 对象的对象的 NetCx 摘要
ms.date: 11/01/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6e8a937b1e79ced499f0263d29977c611bd2cc1c
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903303"
---
# <a name="summary-of-netadaptercx-objects"></a>NetAdapterCx 对象的摘要

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

下图显示了 NetAdapterCx 对象的默认父-子关系。 父对象是图的顶部中，因此，对于示例 NETADAPTER 对象，默认情况下，WDFDEVICE 对象的子级。 可以有多个实例的对象是以双精度框表示。

![NetAdapterCx 客户端驱动程序的对象的 NetAdapterCx 摘要](images/netcx-adapter-object-model.png "NetAdapterCx 客户端驱动程序的摘要的 NetAdapterCx 对象")

WDFDEVICE 对象是一种标准[framework 对象](../wdf/wdf-objects.md)表示的设备。 NETADAPTER 对象表示是网络的所有 i/o 操作的终结点的网络接口。 可以有多个每 WDFDEVICE，与在父对象的每个 NETADAPTER WDFDEVICE NETADAPTER 对象。

大多数网络接口卡 (NIC) 驱动程序只能有一个 NETADAPTER 为其物理设备，但如果他们管理的服务器 NIC 有多个槽，某些客户端驱动程序可能具有多个 NETADAPTER。 例如，[移动宽带 WDF 类扩展 (MBBCx)](mobile-broadband-mbb-wdf-class-extension-mbbcx.md)客户端驱动程序可能管理多个 NETADAPTER 对象，每个元素表示附加的数据包数据协议 (PDP) 上下文。 

必须初始化 NETADAPTER 对象，并将其从客户端驱动程序内创建[ *EVT_WDF_DRIVER_DEVICE_ADD* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add
)通过调用回调函数[ **NetAdapterInitAllocate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterinitallocate)并[ **NetAdapterCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptercreate)。 然后，它必须从启动中的驱动程序[ *EVT_WDF_DEVICE_PREPARE_HARDWARE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)通过调用回调函数[ **NetAdapterStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart). 然后再调用**NetAdapterStart**，驱动程序可以根据需要设置适配器的功能，例如链接层功能、 电源功能、 数据路径功能，接收缩放功能，以及硬件卸载功能。

有关详细信息之间的关系[ **NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet)，并[ **NET_FRAGMENT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netpacket/ns-netpacket-_net_packet_fragment)对象，请参阅[数据包描述符和扩展](packet-descriptors-and-extensions.md)。 有关详细信息**NET_RING**对象，请参阅[Net 环和 net 环迭代器](net-rings-and-net-ring-iterators.md)。
