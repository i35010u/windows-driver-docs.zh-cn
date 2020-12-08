---
title: SR-IOV 物理功能 (PF)
description: SR-IOV 物理功能 (PF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35efc897f8a10f9dff44a4e328f9b892042412d1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834317"
---
# <a name="sr-iov-physical-function-pf"></a>SR-IOV 物理功能 (PF)


物理函数 (PF) 是支持单个根 i/o 虚拟化 (SR-IOV) 接口的 PCI Express (PCIe) 函数。 PF 在 PCIe 配置空间中包括 SR-IOV 扩展功能。 此功能用于配置和管理网络适配器的 SR-IOV 功能，例如启用虚拟化并公开 PCIe 虚拟功能 (VFs) 。

PF 作为 Hyper-v 父分区的管理操作系统中的虚拟网络适配器公开。 PF 微型端口驱动程序是一个 NDIS 微型端口驱动程序，用于管理管理操作系统中的 PF。 将 VFs 的配置和设置以及其他硬件和软件资源与支持 VFs 的其他硬件和软件资源一起使用，可通过 PF 微型端口驱动程序执行。 PF 微型端口驱动程序使用传统的 NDIS 微型端口驱动程序功能，提供对管理操作系统的网络 i/o 资源的访问权限。 PF 驱动程序还用作一种方法，用于管理为 VFs 在适配器上分配的资源。

PF 支持其 PCIe 配置空间中的 SR-IOV 扩展功能结构。 此结构是在 PCI SIG [单根 I/o 虚拟化和共享 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742) 规范中定义的。 此结构包含以下成员：

<a href="" id="totalvfs"></a>**TotalVFs**  
一个只读字段，该字段指定可与 PF 相关联的 VFs 的最大数目。

<a href="" id="numvfs"></a>**NumVFs**  
一个读写字段，该字段指定 SR-IOV 网络适配器上可用的 VFs 的当前数目。

<a href="" id="sr-iov-control"></a>**SR-IOV 控件**  
一个读写字段，它指定在网络适配器上启用或禁用 SR-IOV 功能的各种控制位。 例如，如果将 " **VF 启用** 位" 设置为 "1"，则可以将 VFs 关联到适配器上的 PF。 如果此位设置为零，则在适配器上禁用 VFs 并且不可见。

PF 还为管理操作系统提供与外部物理网络通信的机制。 PF 提供连接到 Hyper-v 可扩展交换机模块的所有虚拟网络适配器的网络连接。 其中包括：

-   提供与 Hyper-v 父分区的网络连接的虚拟网络适配器。

-   虚拟网络适配器，提供与未分配到 VFs 的 Hyper-v 子分区建立网络连接的虚拟网络适配器。

PF 微型端口驱动程序负责管理网络适配器上一个或多个 VFs 使用的资源。 因此，在为 VF 分配任何资源之前，会在管理操作系统中加载 PF 微型端口驱动程序。 释放为 VFs 分配的所有资源后，将停止 PF 微型端口驱动程序。

 

 





