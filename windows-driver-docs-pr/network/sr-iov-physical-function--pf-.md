---
title: SR-IOV 物理功能 (PF)
description: SR-IOV 物理功能 (PF)
ms.assetid: 176ABEA4-B6BE-41D6-9171-8E9A537F8CA1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 376c366a2e198c04a9d08f7f952706b749c94625
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346012"
---
# <a name="sr-iov-physical-function-pf"></a>SR-IOV 物理功能 (PF)


物理函数 (PF) 是支持单根 I/O 虚拟化 (SR-IOV) 接口的网络适配器的 PCI Express (PCIe) 函数。 PF PCIe 配置空间中包括的 SR-IOV 扩展功能。 此功能用于配置和管理网络适配器，如启用虚拟化和公开 PCIe 虚函数 (VFs) 的 SR-IOV 功能。

PF 公开为管理操作系统的 HYPER-V 父分区中的虚拟网络适配器。 PF 微型端口驱动程序是管理中管理操作系统 PF NDIS 微型端口驱动程序。 PF 微型端口驱动程序执行的配置和预配的 VFs，以及为了 VFs，支持其他硬件和软件资源。 PF 微型端口驱动程序使用传统的 NDIS 微型端口驱动程序功能提供对管理操作系统的网络 I/O 资源的访问权限。 PF 驱动程序还用作一种方法来管理适配器上为 VFs 分配的资源。

PF 支持 SR-IOV 扩展功能结构中其 PCIe 配置空间。 此结构定义中 PCI SIG[单根 I/O 虚拟化和共享 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742)规范。 此结构包括以下成员：

<a href="" id="totalvfs"></a>**TotalVFs**  
只读字段，用于指定可以与 PF.相关联 VFs 的最大数目

<a href="" id="numvfs"></a>**NumVFs**  
读写字段，用于指定的 VFs SR-IOV 网络适配器上可用的当前数目。

<a href="" id="sr-iov-control"></a>**SR-IOV 控件**  
指定启用或禁用网络适配器上的 SR-IOV 功能的各种控制位的读写字段。 例如，如果**VF 启用**位设置为其中一个，可以与在适配器上 PF 相关联 VFs。 如果此位设置为零，VFs 是禁用，并且在适配器上不可见。

PF 还提供了用于管理操作系统与外部的物理网络进行通信的机制。 PF 提供与连接到 HYPER-V 可扩展交换机模块的所有虚拟网络适配器的网络连接。 这包括以下内容：

-   与 HYPER-V 父分区建立网络连接的虚拟网络适配器。

-   提供网络连接到 HYPER-V 子分区的虚拟网络适配器没有分配给它们的 VFs。

PF 微型端口驱动程序负责管理由一个或多个虚拟网络适配器上的资源。 正因为如此，PF 微型端口驱动程序之前为 VF 分配任何资源的管理操作系统中加载。 PF 微型端口驱动程序将停止后释放已分配给 VFs 的所有资源。

 

 





