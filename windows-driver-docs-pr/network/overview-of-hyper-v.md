---
title: Hyper-V 概述
description: Hyper-V 概述
ms.assetid: 2D77B1EB-6320-4609-B8EE-236EA75BEADE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac26f781a8f700f6af5ab7e0cf1beb10208679d5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376311"
---
# <a name="overview-of-hyper-v"></a>Hyper-V 概述


HYPER-V 是一种基于虚拟机监控程序的虚拟化技术的 x64 版本的 Windows Server 2008 和更高版本的 Windows Server。 虚拟机监控程序是允许多个独立的操作系统共享单个硬件平台的特定于处理器的虚拟化平台。

HYPER-V 支持通过单独隔离*分区*。 分区是虚拟机监控程序支持的逻辑隔离单元，其中将会运行操作系统。 虚拟化堆栈的 HYPER-V 父分区中，在管理操作系统中运行，并直接访问硬件设备。 然后，管理操作系统创建 HYPER-V 子分区，并启动来宾操作系统中。

分区无法访问物理处理器，也无法处理处理器中断。 但它们具有处理器虚拟视图，并可在专用于每个来宾分区的虚拟内存地址区域中运行。 虚拟机监控程序会处理处理器中断，并且会将中断重定向到各自的分区。 HYPER-V 还可以通过使用 I/O 内存管理单元 (IOMMU) 的操作由处理器使用的内存管理硬件无关的各种来宾虚拟地址空间之间硬件加速的地址转换。 IOMMU 用于将物理内存地址重新映射到子分区所使用的地址。

子分区还没有直接访问其他硬件资源。 相反，子分区提供的资源，名为的虚拟视图*虚拟设备*。 通过虚拟机总线 (VMBus) 或管理操作系统，在父分区中，处理设备请求到虚拟机监控程序，则将重定向到虚拟设备的请求。 VMBus 是逻辑内分区通信通道，与为父分区和子分区之间的通信分配单独的通道。

通过 VMBus 以处理来自子分区的设备访问请求的通信管理操作系统的主机虚拟服务提供商 (Vsp)。 子分区上的来宾操作系统系统承载虚拟服务客户端 (Vsc) 的设备将请求重定向到 Vsp 中管理操作系统使用 VMBus。

为网络访问子分区，网络 VSC (NetVSC) 在来宾操作系统中运行。 每个 NetVSC 和在管理操作系统中运行网络 VSP 之间发送网络请求和数据包。 NetVSC 还公开了物理网络适配器的主机计算机上的虚拟化的视图。 此虚拟化的网络适配器被称为*合成网络适配器*。

**请注意**  HYPER-V 还支持另一个名为的效率较低的虚拟化的网络适配器*仿真的网络适配器*。 仿真的网络适配器模仿 Intel 网络适配器，并使用硬件仿真转发数据包与 NetVSP。

 

下图显示网络的数据路径中的 HYPER-V 通过合成网络适配器。

![综合网络的设备数据路径中的 hyper-v](images/vmqsyntheticpaths.png)

通过使用虚拟化的 NDIS 网络接口，如虚拟机队列 (VMQ)、 单根 I/O 虚拟化 (SR-IOV) 或 HYPER-V 可扩展交换机接口，这些数据路径进行了扩展。 例如，NetVSC 无法配置为连接到虚拟函数 (VF) 的支持 SR-IOV 接口的物理网络适配器。 在这种情况下，NetVSC 发送和接收数据包，直接通过基础物理适配器并不是其在 VMBus 上。

有关 HYPER-V 的详细信息，请参阅[HYPER-V](https://go.microsoft.com/fwlink/p/?linkid=217079)。

 

 





