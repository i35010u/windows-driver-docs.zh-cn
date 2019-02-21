---
title: 在 2.0 中 WDDM 的 GPU 虚拟内存
description: 本部分提供有关 GPU 虚拟内存，包括已进行了更改的原因和驱动程序将使用它的详细信息。
ms.assetid: 88A99A31-9B84-4594-8A93-1C2783F7390D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4a848311cbb7e802b970bcc11598e9d96a23f90
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547016"
---
# <a name="gpu-virtual-memory-in-wddm-20"></a>在 2.0 中 WDDM 的 GPU 虚拟内存


本部分提供有关 GPU 虚拟内存，包括已进行了更改的原因和驱动程序将使用它的详细信息。 此功能可从 Windows 10 开始。

## <a name="span-idintroductionspanspan-idintroductionspanspan-idintroductionspanintroduction"></a><span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>简介


Windows 显示器驱动程序模型 (WDDM) v1.x 中，在设备驱动程序接口 (DDI) 是构建这样的图形处理单元 (GPU) 引擎应引用通过段物理地址的内存。 应用程序间共享和额外提交段时，资源获取其生存期通过重新定位，并更改其已分配的物理地址。 这会导致需要跟踪内存分配和修补程序位置列表中，通过命令缓冲区内的引用并修补这些缓冲区与正确的物理内存引用之前提交到 GPU 引擎。 这种跟踪和修补开销很高，实质上是施加了其中的视频内存管理器必须检查每个数据包，然后将提交到引擎的计划模型。

随着更多的硬件供应商向基于硬件计划工作到 GPU 提交直接从用户模式下的模型和 GPU 管理工作本身的各种队列，其中有必要消除对要检查的视频内存管理器的需要和修补程序发布到 GPU 引擎在提交之前每个命令缓冲区。

若要实现此目的，我们引入对 GPU 虚拟 WDDM v2 中的寻址的支持。 在此模型中，每个进程获取分配唯一的 GPU 虚拟地址空间中的每个 GPU 上下文中执行。 分配，由一个进程，创建或打开获取分配唯一分配的生存期内保持常量和唯一该进程 GPU 虚拟地址空间中的 GPU 虚拟地址。 这允许用户模式驱动程序通过其 GPU 虚拟地址的引用分配而无需担心通过其生存期内更改的基础物理内存。

单独的 GPU 引擎可以在物理或虚拟模式下运行。 在物理模式下，计划模型保持不变这一点与 WDDM 1.x 版。 在物理模式下用户模式驱动程序将继续生成分配和修补位置列表。 它们沿命令缓冲区提交，并用于映射到修补程序之前提交到引擎的实际物理地址的命令缓冲区。

处于虚拟模式下，引擎引用通过 GPU 虚拟地址的内存。 在此模式下用户模式驱动程序直接从用户模式下生成命令缓冲区，并使用新服务将这些命令提交到内核。 在此模式下用户模式驱动程序不会生成分配或修补尽管仍负责管理分配的驻留位置列表。 有关驱动程序驻留的详细信息，请参阅[WDDM 2.0 中的驱动程序驻留](driver-residency-in-wddm-2-0.md)。

## <a name="span-idgpumemorymodelsspanspan-idgpumemorymodelsspanspan-idgpumemorymodelsspangpu-memory-models"></a><span id="GPU_memory_models"></span><span id="gpu_memory_models"></span><span id="GPU_MEMORY_MODELS"></span>GPU 内存模型


WDDM v2 支持两个不同的模型适用 GPU 虚拟寻址*GpuMmu*并*IoMmu*。 驱动程序必须参加以支持一个或两个模型。 单个 GPU 节点可以同时支持这两种模式。

<span id="GpuMmu_model"></span><span id="gpummu_model"></span><span id="GPUMMU_MODEL"></span>GpuMmu 模型  
在中*GpuMmu*模型，视频内存管理器管理的 GPU 内存管理单元和基础页面表，并公开允许它管理 GPU 虚拟地址映射到分配给用户模式驱动程序服务。

有关详细信息，请参阅[GpuMmu 模型](gpummu-model.md)。

<span id="IoMmu_model"></span><span id="iommu_model"></span><span id="IOMMU_MODEL"></span>IoMmu 模型  
在中*IoMmu*模型、 CPU 和 GPU 共享常见的地址空间和页表。

有关详细信息，请参阅[IoMmu 模型](iommu-model.md)。

 

 





