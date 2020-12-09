---
title: 单根 I/O 虚拟化 (SR-IOV) 概述
description: 单根 I/O 虚拟化 (SR-IOV) 概述
ms.date: 11/17/2020
ms.localizationpriority: medium
ms.custom: contperf-fy21q2
ms.openlocfilehash: c2ad2713143e7deb84eeee7ddd22ed1afaf64436
ms.sourcegitcommit: 66043df62672b79a8f9fcb0bc2deb26b8f182fb6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "96912435"
---
# <a name="overview-of-single-root-io-virtualization-sr-iov"></a>单根 I/O 虚拟化 (SR-IOV) 概述


 (SR-IOV) 接口的单个根 i/o 虚拟化是 PCI Express (PCIe) 规范的扩展。 SR-IOV 允许设备（如网络适配器）在各种 PCIe 硬件功能之间分离对其资源的访问。 这些函数包含以下类型：

* [PCIe 物理功能 (PF) ](sr-iov-physical-function--pf-.md)。 此函数是设备的主要功能，可公布设备的 SR-IOV 功能。 PF 与虚拟化环境中的 Hyper-v 父分区关联。

* 一个或多个 [PCIe 虚拟函数 (VFs) ](sr-iov-virtual-functions--vfs-.md)。 每个 VF 与设备的 PF 关联。 VF 与设备上的 PF 和其他 VFs 共享设备的一个或多个物理资源，如内存和网络端口。 每个 VF 都与虚拟化环境中的 Hyper-v 子分区关联。

为每个 PF 和 VF 分配一个唯一的 PCI Express 请求者 ID (RID) ，该 ID 允许 i/o 内存管理单元 (IOMMU) 区分不同的流量流，并在 PF 与 VFs 之间应用内存和中断转换。 这允许流量流直接传递到适当的 Hyper-v 父分区或子分区。 因此，非特权数据流量将从 PF 流向 VF，而不会影响其他 VFs。

SR-IOV 使网络流量能够绕过 Hyper-v 虚拟化堆栈的软件交换机层。 由于 VF 分配给子分区，因此网络流量直接在 VF 和子分区之间流动。 因此，软件仿真层中的 i/o 开销会降低，并实现与 nonvirtualized 环境中几乎相同的性能。

有关详细信息，请参阅下列主题：

[SR-IOV 体系结构](sr-iov-architecture.md)

[SR-IOV 数据路径](sr-iov-data-paths.md)

 

 





