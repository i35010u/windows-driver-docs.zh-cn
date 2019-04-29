---
title: 单根 I/O 虚拟化 (SR-IOV) 概述
description: 单根 I/O 虚拟化 (SR-IOV) 概述
ms.assetid: B241F468-F568-4500-9356-E576CEBA8F3B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba74bd92a204a7828e85239ff1e142a1d405b9a7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381326"
---
# <a name="overview-of-single-root-io-virtualization-sr-iov"></a>单根 I/O 虚拟化 (SR-IOV) 概述


单根 I/O 虚拟化 (SR-IOV) 接口是 PCI Express (PCIe) 规范的扩展。 SR-IOV 允许的设备，如网络适配器，将在各种 PCIe 硬件函数及其资源的访问权限。 这些函数包括以下类型：

-   PCIe 物理函数 (PF)。 此函数是设备的主要功能，并且将公布设备的 SR-IOV 功能。 PF 是与虚拟化环境中的 HYPER-V 父分区相关联。

-   一个或多个 PCIe 虚函数 (VFs)。 每个 VF 程序与设备的 PF. VF 与 PF 和其他 VFs 在设备上的共享设备，例如内存和网络端口，一个或多个物理的资源。 每个 VF 是与虚拟化环境中的 HYPER-V 子分区相关联。

每个 PF 和 VF 分配唯一 PCI Express 请求者 ID (RID)，允许 I/O 内存管理单元 (IOMMU) 来区分不同的流量流和应用内存和中断 PF 与 VFs 之间的转换。 这样，被直接发送到相应的 HYPER-V 父或子分区的流量流。 因此，非特权的数据流量会流向从 PF VF 而不会影响其他 VFs。

SR-IOV 允许网络流量绕过 HYPER-V 虚拟化堆栈的软件切换层。 由于 VF 分配给子分区中，网络之间的流量直接 VF 和子分区。 结果是，I/O 开销在软件仿真层就会降低，实现性能与非虚拟化环境几乎相同的网络性能。

有关详细信息，请参阅下列主题：

[SR-IOV 体系结构](sr-iov-architecture.md)

[SR-IOV 数据路径](sr-iov-data-paths.md)

 

 





