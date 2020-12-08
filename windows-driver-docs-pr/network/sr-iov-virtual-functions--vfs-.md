---
title: SR-IOV 虚拟功能 (VF)
description: SR-IOV 虚拟功能 (VF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 726f38a861a5a523a1f2d38343440cf6de7377a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782131"
---
# <a name="sr-iov-virtual-functions-vfs"></a>SR-IOV 虚拟功能 (VF)


PCI Express (PCIe) 虚函数 (VF) 是网络适配器上的轻量 PCIe 功能，支持单个根 i/o 虚拟化 (SR-IOV) 。 VF 与网络适配器上 (PF) 的 PCIe 物理函数关联，表示网络适配器的虚拟化实例。 每个 VF 都有其自己的 PCI 配置空间。 每个 VF 还将网络适配器上的一个或多个物理资源（例如外部网络端口）与 PF 和其他 VFs 共享。

VF 不是完备的 PCIe 设备。 但是，它提供了在 Hyper-v 子分区和基础 SR-IOV 网络适配器之间直接传输数据的基本机制。 与数据传输关联的软件资源直接可用于 VF，并独立于其他 VFs 或 PF 使用。 但是，大多数这些资源的配置是通过在 Hyper-v 父分区的管理操作系统中运行的 PF 微型端口驱动程序来执行的。

VF 作为虚拟网络适配器 (*vf 网络适配器*) 在 hyper-v 子分区中运行的来宾操作系统中。 VF 与 SR-IOV 网络适配器的 NIC 交换机上的虚拟端口 (VPort) 相关联后，在 VM 中运行的虚拟 PCI (VPCI) 驱动程序将公开 VF 网络适配器。 公开后，来宾操作系统中的 PnP 管理器会加载 VF 微型端口驱动程序。

**注意**  Hyper-v 子分区也称为 *虚拟机 (VM)*。

 

VF 微型端口驱动程序是 VM 中安装的用于管理 VF 的 NDIS 微型端口驱动程序。 由 VF 微型端口驱动程序执行的任何操作都不得影响同一网络适配器上的任何其他 VF 或 PF。

VF 微型端口驱动程序可以像任何 PCI 设备驱动程序一样工作。 它可以读取和写入 VF 的 PCI 配置空间。 但是，对虚拟 PCI 设备的访问权限是一项特权操作，由 PF 微型端口驱动程序通过以下方式进行管理：

-   当 VF 微型端口驱动程序调用 [**NdisMGetBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetbusdata) 从 VF 网络适配器的 PCI 配置空间读取数据时，会通知虚拟化堆栈。 此堆栈在 Hyper-v 父分区的管理操作系统中运行。 当通知堆栈读取请求时，它会发出对象标识符 (oid) 方法请求（oid [ \_ SRIOV \_ \_ \_ \_ ](./oid-sriov-read-vf-config-space.md) ）。 要读取的数据是在 OID 请求中包含的 [**NDIS \_ SRIOV \_ 读取 \_ VF \_ 配置 \_ 空间 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_read_vf_config_space_parameters) 结构中指定的。

    该驱动程序从 VF PCI 配置空间读取请求的数据，并通过完成 OID 请求来返回数据。 在对 [**NdisMGetBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetbusdata) 的调用完成时，此数据将返回到 VF 微型端口驱动程序。

-   当 VF 微型端口驱动程序调用 [**NdisMSetBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetbusdata) 将数据写入 VF 网络适配器的 PCI 配置空间时，虚拟化堆栈会收到写入请求的通知。 它发出 oid [ \_ SRIOV 将 \_ \_ VF \_ 配置 \_ 空间写入](./oid-sriov-write-vf-config-space.md) 到 PF 微型端口驱动程序的 oid 方法请求。 要写入的数据是在 OID 请求中包含的 [**NDIS \_ SRIOV \_ 写入 \_ VF \_ 配置 \_ 空间 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_write_vf_config_space_parameters) 结构中指定的。

    驱动程序将数据写入 VF PCI 配置空间，并在完成 OID 请求时返回请求的状态。 调用 [**NdisMSetBusData**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetbusdata) 完成后，此状态将返回到 VF 微型端口驱动程序。

VF 微型端口驱动程序也可能与 PF 微型端口驱动程序通信。 此通信路径位于 backchannel 接口上。 有关详细信息，请参阅 [SR-IOV PF/VF Backchannel 通信](sr-iov-pf-vf-backchannel-communication.md)。

**注意**  VF 微型端口驱动程序必须知道它正在虚拟化环境中运行，以便它可以与 PF 小型传输驱动程序通信以执行特定操作。 有关驱动程序如何执行此操作的详细信息，请参阅 [初始化 VF 微型端口驱动程序](initializing-a-vf-miniport-driver.md)。

 

 

