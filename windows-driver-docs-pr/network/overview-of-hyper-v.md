---
title: Hyper-V 概述
description: Hyper-V 概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd6ff7a96bb85e62e23263a4b08964e3aa3f8c02
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801387"
---
# <a name="overview-of-hyper-v"></a>Hyper-V 概述


Hyper-v 是一种基于虚拟机监控程序的虚拟化技术，适用于 x64 版本的 windows Server 2008 和更高版本的 Windows Server。 虚拟机监控程序是特定于处理器的虚拟化平台，允许多个独立的操作系统共享单个硬件平台。

Hyper-v 通过单独的 *分区* 支持隔离。 分区是虚拟机监控程序支持的逻辑隔离单元，其中将会运行操作系统。 虚拟化堆栈在 Hyper-v 父分区的管理操作系统中运行，并可直接访问硬件设备。 然后，管理操作系统会创建 Hyper-v 子分区并在其中启动来宾操作系统。

分区无法访问物理处理器，也无法处理处理器中断。 但它们具有处理器虚拟视图，并可在专用于每个来宾分区的虚拟内存地址区域中运行。 虚拟机监控程序会处理处理器中断，并且会将中断重定向到各自的分区。 Hyper-v 也可以通过使用 i/o 内存管理单元 (IOMMU) 在不同的来宾虚拟地址空间之间进行地址转换，这种方式与处理器所使用的内存管理硬件无关。 IOMMU 用于将物理内存地址重新映射到子分区所使用的地址。

子分区也不能直接访问其他硬件资源。 相反，子分区显示资源的虚拟视图，称为 *虚拟设备*。 向虚拟设备发出的请求将通过虚拟机总线 (VMBus) 或虚拟机监控程序（用于处理设备请求的父分区中的管理操作系统）进行重定向。 VMBus 是逻辑分区间通信通道，为父分区和子分区之间的通信分配了单独的通道。

管理操作系统将虚拟服务提供商 (.Vsps) ，该服务提供商通过 VMBus 通信来处理子分区的设备访问请求。 子分区上的来宾操作系统使用 VMBus 将虚拟服务客户端 (Vsc) ，以将设备请求重定向到管理操作系统中的 .Vsps。

对于对子分区的网络访问， (Netvsc.sys) 的网络 VSC 在来宾操作系统中运行。 网络请求和数据包在每个 Netvsc.sys 和在管理操作系统中运行的网络 VSP 之间发送。 Netvsc.sys 还公开了主机上物理网络适配器的虚拟化视图。 此虚拟化网络适配器称为 *合成网络适配器*。

**注意**  Hyper-v 还支持另一种不太有效的虚拟化网络适配器，称为 *仿真网络适配器*。 仿真网络适配器模拟 Intel 网络适配器，并使用硬件仿真将数据包转发到 NetVSP，并将数据包转发到该网络适配器。

 

下图显示了 Hyper-v over 合成网络适配器的网络数据路径。

![hyper-v 中的综合网络设备数据路径](images/vmqsyntheticpaths.png)

使用 NDIS 虚拟化网络接口扩展这些数据路径，例如虚拟机队列 (VMQ) 、单一根 i/o 虚拟化 (SR-IOV) 或 Hyper-v 可扩展交换机接口。 例如，可以将 Netvsc.sys 配置为连接到支持 SR-IOV 接口的物理网络适配器 (VF) 的虚拟函数。 在这种情况下，Netvsc.sys 直接在基础物理适配器上发送和接收数据包，而不是通过 VMBus 发送和接收数据包。

有关 Hyper-v 的详细信息，请参阅 [hyper-v](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753637(v=ws.10))。

 

