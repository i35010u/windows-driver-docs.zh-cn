---
title: 虚拟功能解除序列
description: 虚拟功能解除序列
ms.assetid: 8C59A4F7-FC5D-4680-8CDD-751422588601
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b321feb096cc65e2298d03cf3991b94ca2e738c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346002"
---
# <a name="virtual-function-teardown-sequence"></a>虚拟功能解除序列


支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器必须能够支持以下硬件组件：

-   一个 PCI Express (PCIe) 物理函数 (PF)。 PF 始终存在于网络适配器上并附加到 HYPER-V 父分区。

    有关此硬件组件的详细信息，请参阅[SR-IOV 物理函数 (PF)](sr-iov-physical-function--pf-.md)。

-   一个或多个 PCIe 虚拟函数 (VF)。 必须初始化每个取景器，并将其来宾操作系统的网络组件才能发送或接收数据包通过取景器附加到 HYPER-V 子分区。

    有关此硬件组件的详细信息，请参阅[SR-IOV 虚拟功能 (VFs)](sr-iov-virtual-functions--vfs-.md)。

在拆解 VF 并释放其资源之前，虚拟化堆栈将通知虚拟 PCI (VPCI) 虚拟服务提供商 (VSP)。 在管理操作系统的 HYPER-V 父分区中运行此 VSP。 此通知告诉 VPCI VSP，将在拆解和从子分区中分离 VF。 VPCI VSP 将通过虚拟机总线 (VMBus) 消息发送到在子分区的来宾操作系统中运行的 VPCI 虚拟服务客户端 (VSC)。 这些消息请求 VPCI VSC 正常删除时 VF 已附加到子分区公开的 VF 网络适配器。 这将导致 NetVSC 从 VF 微型端口驱动程序和驱动程序要暂停取消绑定。 在此情况下，子分区中的数据包流量 VF 数据路径中迁移到基于软件的综合数据路径。 有关这些数据路径的详细信息，请参阅[SR-IOV 数据路径](sr-iov-data-paths.md)。

完成故障转移到的综合数据路径后，VF 被撤销，释放其资源。 下图显示了与 VF 拆卸涉及的步骤。

![显示来自虚拟化堆栈的调用到 ndis，再到 pf 微型端口驱动程序的示例 vf 拆卸序列](images/sriov-vf-teardown.png)

NDIS、 虚拟化堆栈和 PF 微型端口驱动程序在 VF 拆卸过程中执行以下步骤：

1.  虚拟化堆栈移动的媒体访问控制 (MAC) 和虚拟 LAN (VLAN) 筛选器的步骤与附加到 PF.此默认虚拟端口 (VPort) 的虚拟机 (VM) 网络适配器 VM 网络适配器的子分区在来宾操作系统中公开。

    筛选器移动到默认 VPort Aftet，综合数据路径是完全可操作的网络流量与来宾操作系统中运行的网络组件。 PF 微型端口驱动程序指示默认 PF VPort 综合数据路径用于指示将数据包用于来宾操作系统上的接收的数据包。 同样，从来宾操作系统的所有传输的数据包是通过综合数据路径路由，并且通过默认 PF VPort 传输。

2.  虚拟化堆栈中删除通过发出的对象标识符 (OID) 组请求附加到 VF VPort [OID\_NIC\_交换机\_删除\_VPORT](https://msdn.microsoft.com/library/windows/hardware/hh451818)到 PF微型端口驱动程序。 微型端口驱动程序释放与 VPort 关联的任何硬件或软件资源并完成 OID 请求。

    有关详细信息，请参阅[删除虚拟端口](deleting-a-virtual-port.md)。

3.  虚拟化堆栈 PCIe 函数级别前重置 (FLR) 的取景器释放其资源的请求。 通过发出的 OID 集请求的堆栈实现这[OID\_SRIOV\_重置\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451889)到 PF 微型端口驱动程序。 FLR VF SR-IOV 网络适配器上引入静止状态，并为 VF 清除任何挂起的中断事件。

4.  虚拟化堆栈 VF 已被重置后，通过发出 OID 集请求的请求的 VF 资源释放[OID\_NIC\_交换机\_免费\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822)到 PF微型端口驱动程序。 这将导致微型端口驱动程序，以释放与 VF 相关联的硬件资源。

 

 





