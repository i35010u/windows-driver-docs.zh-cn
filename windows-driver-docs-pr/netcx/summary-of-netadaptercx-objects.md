---
title: NetAdapterCx 对象的摘要
description: NetAdapterCx 对象的摘要
ms.assetid: 1635C737-42C6-4957-A3E0-1184A5545441
keywords:
- NetAdapterCx 对象的摘要，NetCx 对象摘要
ms.date: 11/01/2018
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: b85201bcf93dbf2a2ff2a45840d95d8a06a4a20d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838270"
---
# <a name="summary-of-netadaptercx-objects"></a>NetAdapterCx 对象的摘要

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

下图显示了 NetAdapterCx 对象的默认父子关系。 父对象位于图形顶部，因此，默认情况下，GET-NETADAPTER 对象是 WDFDEVICE 对象的子对象。 可以具有多个实例的对象由双框表示。

![NetAdapterCx 客户端驱动程序的 NetAdapterCx 对象摘要](images/netcx-adapter-object-model.png "NetAdapterCx 客户端驱动程序的 NetAdapterCx 对象摘要")

WDFDEVICE 对象是表示设备的标准[框架对象](../wdf/wdf-objects.md)。 GET-NETADAPTER 对象表示一个网络接口，该接口是所有网络 i/o 的终结点。 每个 WDFDEVICE 可以有多个 GET-NETADAPTER 对象，WDFDEVICE 是每个 GET-NETADAPTER 的父对象。

大多数网络接口卡（NIC）驱动程序的物理设备仅有一个 GET-NETADAPTER，但如果它们管理具有多个槽的服务器 NIC，则某些客户端驱动程序可能会有多个 GET-NETADAPTER。 例如，[移动宽带 WDF 类扩展（MBBCx）](mobile-broadband-mbb-wdf-class-extension-mbbcx.md)客户端驱动程序可能会管理多个 get-netadapter 对象，每个对象表示一个额外的数据包数据协议（PDP）上下文。 

必须通过调用[**NetAdapterInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterinitallocate)和[**NetAdapterCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptercreate)，在客户端驱动程序的[*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数内初始化和创建 get-netadapter 对象。 然后，必须通过调用[**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)从驱动程序的[*EVT_WDF_DEVICE_PREPARE_HARDWARE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数中启动它。 在调用**NetAdapterStart**之前，驱动程序可以选择设置适配器的功能，如链接层功能、电源功能、数据路径功能、接收缩放功能和硬件卸载功能。

有关[**NET_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet)和[**NET_FRAGMENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netpacket/ns-netpacket-_net_packet_fragment)对象之间的关系的详细信息，请参阅[数据包描述符和扩展](packet-descriptors-and-extensions.md)。 有关**NET_RING**对象的详细信息，请参阅[净环和网络环迭代](net-rings-and-net-ring-iterators.md)器。
