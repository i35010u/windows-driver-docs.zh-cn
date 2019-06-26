---
title: 64KB 页面支持
description: 为了支持 64KB 页 Windows 显示器驱动程序模型 (WDDM) v2 提供了两种类型的叶页表，一个支持 4 KB 页表项，另一个支持 64 kb。
ms.assetid: 24D4854E-BBD7-46A9-8FEF-EF13D2968E6B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5984d481dbf71dcd5879f884b291d793be4323b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353842"
---
# <a name="support-for-64kb-pages"></a>64KB 页面支持


为了支持 64KB 页 Windows 显示器驱动程序模型 (WDDM) v2 提供了两种类型的叶页表，一个支持 4 KB 页表项，另一个支持 64 kb。 这两个页表条目的大小涵盖的相同的虚拟地址范围，因此 4 KB 页的页表具有 16 倍的条目数为 64 KB 的页表。

由定义的 64KB 页表大小[ **DXGK\_GPUMMUCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gpummucaps)::**LeafPageTableSizeFor64KPagesInBytes**。

[ *UpdatePageTable* ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)操作的一个标志，指示更新的页表类型时， [ **DXGK\_UPDATEPAGETABLEFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_updatepagetableflags)::**Use64KBPages**。

有两种模式的 WDDM v2 支持的操作：

1.  级别 1 页表页表项点到 4 KB 的页表或 64KB 页表。
2.  在同一时间，第 1 级页表的页表条目指向 4 KB 的页表和 64 KB 的页表。 这称为"双 PTE"模式。

*双 PTE*表示支持[ **DXGK\_GPUMMUCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gpummucaps)::**DualPteSupported**上限。
视频内存管理器会选择基于分配对齐方式、 图形处理单元 (GPU) 内存段属性和 GPU 内存的段类型的页大小。 将使用 64 KB 页为单位，如果其对齐和大小是多个映射分配 64 KB，并且是支持 64 KB 页为单位的内存段中。

## <a name="span-idsingleptemodespanspan-idsingleptemodespanspan-idsingleptemodespansingle-pte-mode"></a><span id="Single_PTE_mode"></span><span id="single_pte_mode"></span><span id="SINGLE_PTE_MODE"></span>单一 PTE 模式


在此模式下的第 1 级页表页表项点到 4 KB 的页表或 64KB 页表。

[**DXGK\_PTE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_dxgk_pte)::**PageTablePageSize**字段添加到**DXGK\_PTE**。 它应仅对第 1 级页表 （页目录中的旧术语） 的页表项。 此字段指示内核模式驱动程序 （使用 64KB 或 4 KB 页） 的相应页表的类型。

视频内存管理器会选择要用于虚拟地址的 64KB 页表时的范围：

-   仅对齐 64 KB 分配内容映射到的范围。
-   映射到范围的所有分配的内存段支持 64 KB 页为单位。

当虚拟地址范围映射由 64KB 页和上述条件都不再有效 （例如，分配是提交到系统内存段），视频内存管理器从 64KB 页表切换到 4 KB 的页表。

当页表具有仅 64KB 页表项和页表项需要指向 4 KB 页面 （例如，分配放置到系统内存），页表将转换为使用 4 KB 页表项。

转换完成，如下所示：

1.  过程的所有上下文都将都挂起。
2.  现有的页表条目更新为指向 4 KB 页为单位。 该驱动程序将获得[ *UpdatePageTable* ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)分页操作。
3.  级别 1 页表条目指向的页表随即更新以反映新的页面大小 (**PageTablePageSize** = **DXGK\_PTE\_页\_表\_页上\_4KB**)。 该驱动程序将获得[ *UpdatePageTable* ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)分页操作。
4.  恢复过程的所有上下文。

当页表具有唯一的 4 KB 页表项，并且必须指向 4 KB 页的页表条目数为零时，将转换的页表为使用 64KB 页表项。

转换完成，如下所示：

1.  过程的所有上下文都将都挂起。
2.  现有的页表条目更新为指向 64 KB 页为单位。 该驱动程序将获得[ *UpdatePageTable* ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)分页操作。
3.  级别 1 页表条目指向的页表随即更新以反映新的页面大小 (**PageTablePageSize** = **DXGK\_PTE\_页\_表\_页上\_64KB**)。 该驱动程序将获得[ *UpdatePageTable* ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)分页操作。
4.  恢复过程的所有上下文。

若要防止频繁切换不同的页表的大小，该驱动程序应打包小的分配在一起。

## <a name="span-iddualptemodespanspan-iddualptemodespanspan-iddualptemodespandual-pte-mode"></a><span id="Dual_PTE_mode"></span><span id="dual_pte_mode"></span><span id="DUAL_PTE_MODE"></span>双 PTE 模式


在此模式下的第 1 级页表页表项可能指向 4 KB 的页表和 64KB 页表在同一时间。

级别 1 页表条目中的这两个指针可能**有效**设置标志，但同时涵盖相同的 64 KB 的虚拟地址范围级别 0 页表中的条目不能为有效。

当分配所涵盖的 64KB 页表项放置到使用 64 KB 的页面大小的内存段时，64KB 页表条目变得无效和相应的 4 KB 页表项变为有效。

下图中的 4 KB 分配和对齐的 64 KB 分配是在级别 0 页表所涵盖的相同虚拟地址范围和支持 64 KB 页为单位的段中。

![双 pte 模式页表](images/support-for-64kb-pages.1.png)

 

 





