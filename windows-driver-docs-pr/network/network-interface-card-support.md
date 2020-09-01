---
title: 网络接口卡支持
description: 网络接口卡支持
ms.assetid: de673a37-3870-4995-b4f1-647b502e0773
keywords:
- 微型端口驱动程序 WDK 网络，NIC 支持
- NDIS 微型端口驱动程序 WDK、NIC 支持
- Nic WDK 网络，类型
- 网络接口卡 WDK 网络，类型
- 总线主控 DMA Nic WDK 网络
- 非总线主机 DMA Nic WDK 网络
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 63514cc68abaf2f78f1e37cf0455b9378e0ef80f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210663"
---
# <a name="network-interface-card-support"></a>网络接口卡支持

本主题描述了 NDIS 微型端口驱动程序可以管理的网络接口卡 (Nic) 的类型，以及不同种类的 Nic 如何影响驱动程序传输网络数据的方式。

## <a name="reporting-a-nics-medium-type-to-ndis"></a>向 NDIS 报告 NIC 的媒介类型

若要报告 NIC 的中等类型，微型端口驱动程序将指针传递到[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数的*MiniportAttributes*参数中的[**NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构。 小型端口驱动程序在初始化期间从其[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用**NdisMSetMiniportAttributes** 。 在设置任何其他属性之前，微型端口驱动程序应设置 *MiniportAttributes* 属性，并设置 [**NDIS \_ 微型端口 \_ 适配器 \_ 注册 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes) 结构中的注册属性。 设置 *MiniportAttributes* 属性是必需的。 设置*MiniportAttributes*属性时，驱动程序将**NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES** **结构的媒体成员设置**为相应的媒体类型。

当过量 NDIS 协议驱动程序调用 [**NdisOpenAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex) 绑定到指定的微型端口适配器时，它将提供可以在其上操作的介质类型的列表。 NDIS 使用微型端口驱动程序和协议驱动程序中的信息来设置绑定。 此绑定提供在驱动程序堆栈中上移和下移网络数据的路径。

## <a name="physical-nics"></a>物理 Nic

小型使用驱动程序驱动程序完成以初始化微型端口适配器并发送和接收网络数据的步骤可能取决于物理设备的功能，如下所示。

- NDIS-WDM Nic

    通过 NDIS-WDM Nic （如基于 USB 的 Nic），微型端口驱动程序用 DMA 管理内存的方式并不重要，并且对其不可见。

- 总线主控 DMA Nic

    这些 Nic 可以通过在不使用主机 CPU 的情况下管理网络和主机内存之间的数据传输的板载 DMA 控制器直接访问主机内存。

    若要发送，微型端口驱动程序将设置 NIC 来映射传出缓冲区。 然后，微型端口驱动程序会导致设备从此内存启动传输。 NIC DMA 控制器将数据从共享系统内存传输到网络，并在发送完成后中断 CPU。 若要接收，DMA 控制器会在向主机发送中断通知之前，将传入数据传输到主机内存。

    总线主控 DMA NIC 通常具有一个板载环形缓冲区，微型端口驱动程序可将其映射到系统内存中的一组缓冲区。 通常，可以对 NIC 进行编程以有效地处理多个数据包。 用于管理此类 NIC 的微型端口驱动程序通常支持 multipacket 发送和接收，因为 NIC 可以有效地处理多个数据包，从而提高其 i/o 吞吐量。

- Nonbusmaster DMA Nic

    目前，nonbusmaster DMA Nic 包括以下各项：

    -   系统 DMA Nic

        管理此类 NIC 的微型端口驱动程序使用系统 DMA 控制器来管理数据包数据与网络之间的传输。 传输数据需要主机 CPU 的合作。

## <a name="virtual-nics-and-miniports"></a>虚拟 Nic 和微型端口

在虚拟机中，NDIS 微型端口驱动程序可以将仅限软件的资源作为虚拟小型端口来管理，也可以管理表示硬件资源的虚拟 NIC。 下表说明了虚拟微型端口和虚拟 NIC 之间的差异。

|   | 虚拟小型端口 | 虚拟 NIC |
| --- | --- | --- |
| 定义 | 映射到软件枚举的 PnP 设备的 NDIS 微型端口驱动程序。 | 由主机 OS 虚拟机监控程序管理的 NIC。 虚拟机监控程序使虚拟机认为它有一些硬件，但物理环境中实际不存在此类硬件。 |
| 有中断 | 否 | 是 |
| 可以使用 DMA | 否 | 是 |
| 由创建或销毁 .。。 | 来宾操作系统 | 主机操作系统 |
| 可以访问来宾 VM 之外 | 否 | 是 |