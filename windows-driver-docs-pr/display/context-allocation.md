---
title: 上下文分配
description: 若要为保存的上下文区域的上下文中分配内存，内核模式驱动程序可以使用通过 DxgkCbCreateContextAllocation 上下文分配。
ms.assetid: DAD08E7F-13F9-4648-A24C-DD9FBA6D490F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2124558087b5d39520be84093f3b91c2343f7d4c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356249"
---
# <a name="context-allocation"></a>上下文分配


若要为保存的上下文区域的上下文中分配内存，内核模式驱动程序可以使用通过上下文分配[ *DxgkCbCreateContextAllocation*](https://msdn.microsoft.com/library/windows/hardware/hh451312)。 一些新功能添加到上下文分配以使其适应新的图形处理单元 (GPU) 的虚拟地址模型。

## <a name="span-idaccessedphysicallyspanspan-idaccessedphysicallyspanspan-idaccessedphysicallyspanaccessedphysically"></a><span id="AccessedPhysically"></span><span id="accessedphysically"></span><span id="ACCESSEDPHYSICALLY"></span>AccessedPhysically


可以指定上下文分配**AccessedPhysically**标志以指示应在一个内存段中连续分配或映射的小孔，如果从系统内存访问分配。

## <a name="span-idassigningagpuvirtualaddresstoacontextallocationspanspan-idassigningagpuvirtualaddresstoacontextallocationspanspan-idassigningagpuvirtualaddresstoacontextallocationspanassigning-a-gpu-virtual-address-to-a-context-allocation"></a><span id="Assigning_a_GPU_virtual_address_to_a_context_allocation"></span><span id="assigning_a_gpu_virtual_address_to_a_context_allocation"></span><span id="ASSIGNING_A_GPU_VIRTUAL_ADDRESS_TO_A_CONTEXT_ALLOCATION"></span>GPU 虚拟地址分配给上下文分配


视频内存管理器公开的新[ *DxgkCbMapContextAllocation* ](https://msdn.microsoft.com/library/windows/hardware/dn906334)服务到内核模式驱动程序分配到上下文分配 GPU 虚拟地址。

上下文分配内容映射到与指定的上下文相关联的应用程序 GPU 虚拟地址空间。

**请注意**  驱动程序应小心，不要上下文分配时要映射到应用程序 GPU 虚拟地址空间直接公开特权的信息。

 

这些服务行为类似于其用户模式相对应。

## <a name="span-idupdatingthecontentofacontextallocationspanspan-idupdatingthecontentofacontextallocationspanspan-idupdatingthecontentofacontextallocationspanupdating-the-content-of-a-context-allocation"></a><span id="Updating_the_content_of_a_context_allocation"></span><span id="updating_the_content_of_a_context_allocation"></span><span id="UPDATING_THE_CONTENT_OF_A_CONTEXT_ALLOCATION"></span>更新上下文分配的内容


一段时间可能有必要为内核模式驱动程序更新上下文分配的内容。 例如，特权 (**AccessedPhysically**，没有 GPU 虚拟映射) 上下文分配可能包含对与特定上下文关联的页目录的引用。 当内核模式驱动程序通过页目录重定位的系统通知[ *DxgkDdiSetRootPageTable*](https://msdn.microsoft.com/library/windows/hardware/dn906342)，内核模式驱动程序可能需要更新该上下文分配的内容。

为此目的的新[ *DxgkCbUpdateContextAllocation*](https://msdn.microsoft.com/library/windows/hardware/dn906336)添加设备驱动程序接口 (DDI)。 此 DDI 排队到视频内存管理器启动上下文分配的更新的请求。 正在更新的上下文分配映射到暂存区域中的视频内存管理器分页过程中，则该驱动程序调用与新*UpdateContextAllocation*分页操作执行上下文的实际更新分配。 从返回的视频内存管理器*DxgkCbUpdateContextAllocation*在更新完成后。

内核模式驱动程序可以将某些专用驱动程序数据传递到其调用之间[ *DxgkCbUpdateContextAllocation* ](https://msdn.microsoft.com/library/windows/hardware/dn906336)及引发*UpdateContextAllocation*分页操作。

 

 





