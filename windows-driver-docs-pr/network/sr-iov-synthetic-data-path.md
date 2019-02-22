---
title: SR-IOV 综合数据路径
description: SR-IOV 综合数据路径
ms.assetid: FB7E57F6-AA99-421D-8344-B76615BD20ED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7ab27fbe1e04a4518925bc08891f24574df8f13
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543973"
---
# <a name="sr-iov-synthetic-data-path"></a>SR-IOV 综合数据路径


当启动 HYPER-V 子分区，并且运行来宾操作系统时，虚拟化堆栈启动网络虚拟服务客户端 (NetVSC)。 NetVSC 公开提供给在来宾操作系统中运行的协议堆栈的一个微型端口驱动程序边缘的虚拟机 (VM) 网络适配器。

NetVSC 也与在 HYPER-V 父分区的管理操作系统中运行的 HYPER-V 可扩展交换机进行通信。 可扩展交换机组件用作网络虚拟服务提供商 (NetVSP)。 NetVSC 和 NetVSP 之间的接口提供的软件数据路径可以称为*综合数据路径*。

下图显示了 SR-IOV 网络适配器上的综合数据路径的组件。

![堆栈关系图显示通过 vmbus 到子分区包含来宾操作系统进行通信的管理父分区下方的 sr-iov 适配器](images/sriovsynthetic-datapaths.png)

如果基础 SR-IOV 网络适配器分配的 PCI Express (PCIe) 虚拟函数 (VFs) 的资源，虚拟化堆栈将将取景器附加到 HYPER-V 子分区。 附加完成后，子分区中的数据包流量会通过硬件优化 VF 数据路径而不是以综合的数据路径。 VF 数据路径的详细信息，请参阅[SR-IOV 数据路径](sr-iov-data-paths.md)。

如果以下条件之一为 true，虚拟化堆栈可能仍会启用 HYPER-V 子分区的综合数据路径：

-   SR-IOV 网络适配器具有 VF 资源不足，无法容纳所有启动 HYPER-V 子分区。 网络适配器上的所有 VFs 都附加到子分区后，剩余分区使用的综合数据路径。

    故障转移到的综合数据路径 VF 数据路径中的过程被称为*VF 故障转移*。

-   VF 已附加到 HYPER-V 子分区，但将变为已分离。 例如，虚拟化堆栈无法分离 VF 从一个子分区并将其附加到另一个子分区。 这可能不是基础的 SR-IOV 网络适配器上有 VF 资源运行的更多的 HYPER-V 子分区时。

-   HYPER-V 子分区的实时迁移到另一台主机。

虽然 SR-IOV 网络适配器上的综合数据路径不不如 VF 数据路径，但它仍可以是硬件进行了优化。 例如，如果一个或多个虚拟端口 (VPorts) 配置并附加到 PCIe 物理函数 (PF)，数据路径可以提供类似于虚拟机队列 (VMQ) 接口的卸载功能。 有关详细信息，请参阅[非默认虚拟端口和 VMQ](nondefault-virtual-ports-and-vmq.md)。

 

 





