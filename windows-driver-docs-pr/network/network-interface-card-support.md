---
title: 网络接口卡支持
description: 网络接口卡支持
ms.assetid: de673a37-3870-4995-b4f1-647b502e0773
keywords:
- 微型端口驱动程序 WDK 网络 NIC 支持
- NDIS 微型端口驱动程序 WDK，NIC 支持
- Nic WDK 网络类型
- 网络接口卡 WDK 网络类型
- 主总线 DMA Nic WDK 网络
- 非主总线 DMA Nic WDK 网络
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5b2aa3ec1d96a52b8d4f3b66d2b1a2b961b30ceb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386324"
---
# <a name="network-interface-card-support"></a>网络接口卡支持

本主题介绍 NDIS 微型端口驱动程序可以管理，以及如何不同种类的 Nic 影响了驱动程序会将网络数据传输的方式的网络接口卡 (Nic) 的类型。

## <a name="reporting-a-nics-medium-type-to-ndis"></a>报告到 NDIS NIC 的介质类型

若要报告 NIC 的介质类型，微型端口驱动程序，将传递一个指向[ **NDIS\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构中*MiniportAttributes*的参数[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)函数。 微型端口驱动程序调用**NdisMSetMiniportAttributes**从其[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)在初始化过程中的函数。 微型端口驱动程序应设置*MiniportAttributes*属性中设置的注册属性后[ **NDIS\_微型端口\_适配器\_注册\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)结构并且之前设置其他属性。 设置*MiniportAttributes*属性是必需的。 驱动程序集**MediaType**的成员**NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES**结构为相应的媒体类型设置时*MiniportAttributes*属性。

当基础的 NDIS 协议驱动程序调用[ **NdisOpenAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenadapterex)要绑定到指定的微型端口适配器，它提供中等类型可以对的列表。 NDIS 使用从微型端口驱动程序和协议驱动程序的信息来设置绑定。 此绑定将向上和向下驱动程序堆栈的网络数据传输提供的路径。

## <a name="physical-nics"></a>物理 Nic

微型端口驱动程序完成初始化的微型端口适配器来发送和接收网络数据的步骤可以依赖于物理设备的功能，如下所示。

- NDIS WDM Nic

    使用 NDIS WDM Nic，例如基于 USB 的 Nic，微型端口驱动程序管理内存使用 DMA 的方式并不重要到 NDIS 和对它都不可见。

- 主总线 DMA Nic

    通过内置的 DMA 控制器管理的网络和主机的内存，而无需使用主机 CPU 之间传输数据的情况下，两个 Nic 可以直接访问主机内存。

    若要发送，微型端口驱动程序将设置为 NIC 将传出缓冲区映射。 微型端口驱动程序然后会导致设备后，若要开始此内存从其传输。 发送完成时，NIC DMA 控制器会将数据传输从网络和中断 CPU 的共享的系统内存。 若要接收，DMA 控制器传入将数据传输到主机内存之前通知中断的主机。

    总线 master DMA NIC 通常具有微型端口驱动程序映射到一组在系统内存中缓冲区载入环形缓冲区。 通常情况下，NIC 可以通过编程来有效地处理有多个数据包。 管理此类 NIC 的微型端口驱动程序通常支持 multipacket 发送和接收因为 NIC 可以有效地处理有多个数据包，从而提高其 I/O 吞吐量。

- Nonbusmaster DMA Nic

    目前，DMA Nic nonbusmaster 如下：

    -   系统 DMA Nic

        管理此类 NIC 的微型端口驱动程序使用系统 DMA 控制器来管理的传入和传出网络数据包数据传输。 数据传输需要主机 CPU 的协作。

## <a name="virtual-nics-and-miniports"></a>虚拟 Nic 和微型端口

在虚拟机中，NDIS 微型端口驱动程序可以作为虚拟微型端口，来管理或者仅限软件的资源或他们可以管理表示硬件资源的虚拟 NIC。 下表说明了虚拟微型端口和虚拟 NIC 之间的差异

|   | 虚拟微型端口 | 虚拟 NIC |
| --- | --- | --- |
| 定义 | 映射到软件枚举即插即用设备 NDIS 微型端口驱动程序。 | 由主机 OS 虚拟机监控程序管理一个 NIC。 虚拟机监控程序可以认为它具有一些硬件，但在现实环境中实际存在任何此类硬件的虚拟机。 |
| 已中断 | 否 | 是 |
| 可以使用 DMA | 否 | 是 |
| 创建或销毁... | 来宾 OS | 主机操作系统 |
| 可以通过外部来宾 VM | 否 | 是 |
