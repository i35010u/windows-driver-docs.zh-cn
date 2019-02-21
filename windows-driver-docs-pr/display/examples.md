---
title: GpuMmu 示例方案
description: 本主题介绍常见使用方案和操作需要实现它们的顺序。
ms.assetid: 30F7D158-3D99-40EE-8FED-48EC1615AC71
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51cf5e6417fdf4ad725cf2e06f9538f76d5e07ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519279"
---
# <a name="gpummu-example-scenarios"></a>GpuMmu 示例方案


本主题介绍常见使用方案和操作需要实现它们的顺序。

这些方案包括：

-   [更新进程的页表项](#updating-page-table-entries-of-a-process)
-   [将分配内容从一个位置传输到另一个](#transferring-allocation-content-from-one-location-to-another)
-   [填充模式的分配](#filling-an-allocation-with-a-pattern)
-   [使分配驻留在系统内存](#making-an-allocation-resident-in-system-memory)
-   [内存管理器控制结构的初始化](#initialization-of-the-memory-manager-control-structures)

## 更新进程的页表项 <a name="updating-page-table-entries-of-a-process"></a>


下面是用于更新页表项将映射分配的属于某个进程 (P) 的物理内存的操作序列。 假设的页表分配已驻留在的图形处理单元 (GPU) 内存段中。

1.  视频内存管理器为根页表分配的进程 P.分配分页进程上下文中的虚拟地址范围
2.  视频内存管理器分配的页表分配的进程 P.分页进程上下文中的虚拟地址范围
3.  视频内存管理器调用[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)与*UpdatePageTable*命令以将分页进程页表项映射到进程 P 页表和页目录。
4.  视频内存管理器调用[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)与*FlushTLB(PagingProcessRootPageTable)* 命令。
5.  视频内存管理器调用[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)与*UpdatePageTable*命令以使用物理地址填充过程页表项信息。
6.  视频内存管理器调用[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)与*FlushTLB （进程 P 根页表）* 命令。
7.  分页缓冲区提交进行分页进程上下文中执行。

![更新进程的页表项](images/examples.1.png)

## 将分配内容从一个位置传输到另一个<a name="transferring-allocation-content-from-one-location-to-another"></a>


当将分配内容从一个位置传输到另一个 （例如下面是操作的顺序。 从本地内存到系统内存）。

1.  视频内存管理器为源分配和目标分配在分页过程虚拟地址暂存区域中的分配的虚拟地址范围。
2.  视频内存管理器调用[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)与*UpdatePageTable*命令。 命令映射到在本地的 GPU 内存的分配物理地址的源虚拟地址范围的分页进程页表项。
3.  视频内存管理器调用[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)与*UpdatePageTable*命令。 该命令将目标虚拟地址的分页进程页表条目映射到系统内存。
4.  视频内存管理器调用[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)与*FlushTLB （分页处理根页表）*。
5.  视频内存管理器调用[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)与*TransferVirtual*命令来执行传输操作中。
6.  分页缓冲区提交到在分页过程上下文中执行 GPU。

![将分配内容从一个位置传输到另一个](images/examples.2.png)

## 填充模式的分配 <a name="filling-an-allocation-with-a-pattern"></a>


当分配需要填充模式时，下面是操作的顺序。

1.  视频内存管理器为在分页过程虚拟地址暂存区域中的目标分配分配的虚拟地址范围。
2.  视频内存管理器调用[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)与*UpdatePageTable*命令。 该命令将映射的目标虚拟地址的分页进程页表项。
3.  视频内存管理器调用[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)与*FlushTLB （分页处理根页表）*。
4.  视频内存管理器调用[ *DxgkDdiBuildPagingBuffer* ](https://msdn.microsoft.com/library/windows/hardware/ff559587)与*FillVirtual*命令来执行该操作。
5.  分页缓冲区提交到在分页过程上下文中执行 GPU。

![填充模式的分配](images/examples.3.png)

## <a name="making-an-allocation-resident-in-system-memory"></a>使分配驻留在系统内存


执行以下操作时[ **D3DKMTMakeResident** ](https://msdn.microsoft.com/library/windows/hardware/dn906775)调用以使分配驻留。 假定应用程序进程页表是驻留在内存中。

在应用程序线程上下文：

1.  分配并将物理系统内存页分配的虚拟地址范围的固定 （如果驻留在系统内存中分配）。
2.  生成应用程序设备的新分页隔离 ID。
3.  提交[ **MakeResident** ](https://msdn.microsoft.com/library/windows/hardware/dn906775)到视频内存管理器命令正常工作线程。
4.  返回到应用程序。

中的视频内存管理器工作线程上下文：

1.  更新 （请参阅上面的相应部分） 的应用程序进程页表项。
2.  如果分配是驻留在本地内存段中，填充了零 （请参阅上面的相应部分） 的分配。
3.  提交*SignalSynchronizationObject*命令到调度器分页隔离 id。

## <a name="initialization-of-the-memory-manager-control-structures"></a>内存管理器控制结构的初始化


<span id="The_paging_process_initialization"></span><span id="the_paging_process_initialization"></span><span id="THE_PAGING_PROCESS_INITIALIZATION"></span>分页进程初始化  

Microsoft DirectX 图形内核时切换到图形设备初始化分页进程虚拟地址空间*D0*电源设备状态

1.  使用创建的分页进程[ *DxgkDdiCreateProcess*](https://msdn.microsoft.com/library/windows/hardware/dn906337)。
2.  使用创建的系统设备[ *DxgkDdiCreateDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559615)。 此时内核模式驱动程序可以保留分页进程地址空间中的虚拟地址范围。
3.  页表分配为分页进程创建。
4.  页表分配将提交到虚拟寻址功能结构中定义的内存段。
5.  [*UpdatePageTable* ](https://msdn.microsoft.com/library/windows/hardware/ff560815)调用操作来初始化页表。

<span id="A_client_process_initialization"></span><span id="a_client_process_initialization"></span><span id="A_CLIENT_PROCESS_INITIALIZATION"></span>客户端进程初始化  

创建一个新进程时，将 DirectX 图形内核：

-   创建初始页面表分配。
-   从进程的第一个分配进行常驻时初始化页表分配。

 

 

