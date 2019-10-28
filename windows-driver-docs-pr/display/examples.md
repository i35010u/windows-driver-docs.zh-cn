---
title: GpuMmu 示例方案
description: 本主题介绍常见的使用方案和实现这些方案所需的操作顺序。
ms.assetid: 30F7D158-3D99-40EE-8FED-48EC1615AC71
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 320e7cb653b1e51803c8a34e911b563508fe0b04
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839703"
---
# <a name="gpummu-example-scenarios"></a>GpuMmu 示例方案


本主题介绍常见的使用方案和实现这些方案所需的操作顺序。

这些方案包括：

-   [更新进程的页表项](#updating-page-table-entries-of-a-process)
-   [将分配内容从一个位置传输到另一个位置](#transferring-allocation-content-from-one-location-to-another)
-   [使用模式填充分配](#filling-an-allocation-with-a-pattern)
-   [在系统内存中创建一个分配](#making-an-allocation-resident-in-system-memory)
-   [内存管理器控件结构的初始化](#initialization-of-the-memory-manager-control-structures)

## 更新进程的页表项<a name="updating-page-table-entries-of-a-process"></a>


下面是更新页表项以便将属于进程（P）的分配映射到物理内存的操作序列。 假设页表分配已驻留在图形处理单元（GPU）内存段中。

1.  视频内存管理器在进程 P 的根页表分配的分页进程上下文中分配虚拟地址范围。
2.  在进程 P 的页表分配的分页过程上下文中，视频内存管理器会分配虚拟地址范围。
3.  视频内存管理器通过*UpdatePageTable*命令调用[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) ，以将分页进程页表项映射到进程 P 页表和页面目录。
4.  视频内存管理器通过*FlushTLB （PagingProcessRootPageTable）* 命令调用[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) 。
5.  视频内存管理器通过*UpdatePageTable*命令调用[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) ，以填充包含物理地址信息的进程页表项。
6.  视频内存管理器通过*FlushTLB （处理 P 根页表）* 命令调用[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) 。
7.  在分页过程上下文中提交用于执行的分页缓冲区。

![更新进程的页表项](images/examples.1.png)

## 将分配内容从一个位置传输到另一个位置<a name="transferring-allocation-content-from-one-location-to-another"></a>


下面是将分配内容从一个位置转移到另一个位置时的操作顺序（例如 从本地内存到系统内存）。

1.  视频内存管理器为源分配和寻呼进程虚拟地址暂存区中的目标分配分配虚拟地址范围。
2.  视频内存管理器通过*UpdatePageTable*命令调用[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) 。 此命令会将源虚拟地址范围的分页进程页表项映射到本地 GPU 内存中的分配物理地址。
3.  视频内存管理器通过*UpdatePageTable*命令调用[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) 。 命令将目标虚拟地址的分页进程页表项映射到系统内存。
4.  视频内存管理器通过*FlushTLB （分页进程根页表）* 调用[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) 。
5.  视频内存管理器使用*TransferVirtual*命令调用[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)以执行传输操作。
6.  分页缓冲区将提交到 GPU，以便在分页过程上下文中执行。

![将分配内容从一个位置传输到另一个位置](images/examples.2.png)

## 使用模式填充分配<a name="filling-an-allocation-with-a-pattern"></a>


下面是需要使用模式填充分配时的操作顺序。

1.  视频内存管理器为分页处理虚拟地址暂存区中的目标分配分配一个虚拟地址范围。
2.  视频内存管理器通过*UpdatePageTable*命令调用[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) 。 此命令映射目标虚拟地址的分页进程页表项。
3.  视频内存管理器通过*FlushTLB （分页进程根页表）* 调用[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) 。
4.  视频内存管理器通过*FillVirtual*命令调用[*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)来执行该操作。
5.  分页缓冲区将提交到 GPU，以便在分页过程上下文中执行。

![使用模式填充分配](images/examples.3.png)

## <a name="making-an-allocation-resident-in-system-memory"></a>在系统内存中创建一个分配


调用[**D3DKMTMakeResident**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtmakeresident)进行分配时，将执行以下操作。 假设应用程序进程页表驻留在内存中。

在应用程序线程上下文中：

1.  为分配虚拟地址范围分配和固定物理系统内存页（如果分配在系统内存中）。
2.  为应用程序设备生成新的页面防护 ID。
3.  将[**MakeResident**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/nf-d3dkmthk-d3dkmtmakeresident)命令提交到视频内存管理器工作线程。
4.  返回到应用程序。

在视频内存管理器工作线程上下文中：

1.  更新 "应用程序进程" 页表项（请参阅上面相应的部分）。
2.  如果分配驻留在本地内存段中，则用零填充分配（请参阅上面的相应部分）。
3.  向具有页面隔离 ID 的计划程序提交*SignalSynchronizationObject*命令。

## <a name="initialization-of-the-memory-manager-control-structures"></a>内存管理器控件结构的初始化


<span id="The_paging_process_initialization"></span><span id="the_paging_process_initialization"></span><span id="THE_PAGING_PROCESS_INITIALIZATION"></span>分页过程初始化  

当图形设备切换到*D0*电源设备状态时，Microsoft DirectX 图形内核将初始化分页进程虚拟地址空间

1.  分页过程是通过[*DxgkDdiCreateProcess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createprocess)创建的。
2.  系统设备是通过[*DxgkDdiCreateDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)创建的。 此时，内核模式驱动程序可以在分页进程地址空间中保留虚拟地址范围。
3.  为分页过程创建页表分配。
4.  页表分配将提交给虚拟寻址功能结构中定义的内存段。
5.  调用[*UpdatePageTable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)操作来初始化页表。

<span id="A_client_process_initialization"></span><span id="a_client_process_initialization"></span><span id="A_CLIENT_PROCESS_INITIALIZATION"></span>客户端进程初始化  

创建新进程时，DirectX 图形内核将：

-   创建初始页表分配。
-   当从进程开始进行第一次分配时，初始化页表分配。

 

 

