---
title: 64KB 页面支持
description: 若要支持 64 KB 页面，Windows 显示驱动程序模型（WDDM） v2 提供两种类型的叶页表，其中一个表支持 4 KB 页表项，另一个支持 64 KB 条目。
ms.assetid: 24D4854E-BBD7-46A9-8FEF-EF13D2968E6B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe3a4e9c2406b3e7cd722bb22cf4ebbb2f973172
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829395"
---
# <a name="support-for-64kb-pages"></a>64KB 页面支持


若要支持 64 KB 页面，Windows 显示驱动程序模型（WDDM） v2 提供两种类型的叶页表，其中一个表支持 4 KB 页表项，另一个支持 64 KB 条目。 页表项大小都涵盖同一虚拟地址范围，因此4KB 页的页表的项数为 64 KB 页表的项数的16倍。

64 KB 页表的大小由[**DXGK\_GPUMMUCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gpummucaps)：：**LeafPageTableSizeFor64KPagesInBytes**定义。

[*UpdatePageTable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)操作具有一个标志，该标志指示更新页表的类型， [**DXGK\_UPDATEPAGETABLEFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_updatepagetableflags)：：**Use64KBPages**。

WDDM v2 支持两种操作模式：

1.  级别1页表的页表项指向 4 KB 页表或 64 KB 页表。
2.  级别1页表的页表项同时指向 4 KB 页表和 64 KB 页表。 这称为 "双 PTE" 模式。

*双重 PTE*支持由[**DXGK\_GPUMMUCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gpummucaps)：：**DualPteSupported** cap 表示。
视频内存管理器根据分配对齐方式、图形处理单元（GPU）内存段属性和 GPU 内存段类型选择页面大小。 如果使用 64 KB 页的对齐方式和大小为 64 KB 的倍数，并且它驻留在支持 64 KB 页的内存段中，则将使用 KB 的页映射分配。

## <a name="span-idsingle_pte_modespanspan-idsingle_pte_modespanspan-idsingle_pte_modespansingle-pte-mode"></a><span id="Single_PTE_mode"></span><span id="single_pte_mode"></span><span id="SINGLE_PTE_MODE"></span>单 PTE 模式


在此模式下，级别1页表的页表项将指向 4 KB 页表或 64 KB 页表。

[**DXGK\_pte**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_dxgk_pte)：：**PageTablePageSize**字段添加到**DXGK\_pte**。 它应仅用于级别1页表的页表项（旧术语中的页目录）。 此字段告知内核模式驱动程序对应页表的类型（使用64KB 或4KB 页）。

当以下情况时，视频内存管理器选择将 64 KB 页表用于虚拟地址范围：

-   只有 64 KB 的分配被映射到此范围。
-   映射到范围的所有分配的内存段支持 64 KB 页。

如果虚拟地址范围由 64 KB 页映射，并且上述条件不再有效（例如，分配被提交给系统内存段），则视频内存管理器将从 64 KB 页表切换到 4 KB 页表。

当页表只有 64 KB 页表项并且页表项需要指向4KB 页时（例如，将分配放到系统内存中时），页表将转换为使用 4 KB 页表项。

转换的完成方式如下：

1.  进程的所有上下文都处于挂起状态。
2.  现有页表项将更新为指向4KB 页。 驱动程序将获取[*UpdatePageTable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)分页操作。
3.  指向页面表的级别1页表项将更新以反映新的页面大小（**PageTablePageSize** = **DXGK\_PTE\_页\_表\_第 4kb**页）。 驱动程序将获取[*UpdatePageTable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)分页操作。
4.  进程的所有上下文都将恢复。

当页表只有4KB 页表项并且必须指向4KB 页的页表项的数目为零时，页表将转换为使用 64 KB 页表项。

转换的完成方式如下：

1.  进程的所有上下文都处于挂起状态。
2.  现有页表项将更新为指向64KB 页。 驱动程序将获取[*UpdatePageTable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)分页操作。
3.  将更新指向页面表的第1级页表项，以反映新的页面大小（**PageTablePageSize** = **DXGK\_PTE\_页\_表\_的 64 kb**）。 驱动程序将获取[*UpdatePageTable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)分页操作。
4.  进程的所有上下文都将恢复。

若要防止在不同的页表大小之间频繁切换，驱动程序应将小型分配打包在一起。

## <a name="span-iddual_pte_modespanspan-iddual_pte_modespanspan-iddual_pte_modespandual-pte-mode"></a><span id="Dual_PTE_mode"></span><span id="dual_pte_mode"></span><span id="DUAL_PTE_MODE"></span>双 PTE 模式


在此模式下，1级页表的页表项可以同时指向 4 KB 页表和 64 KB 页表。

第1级页表的条目中的两个指针都可能设置了**有效**的标志，但属于同一 64 KB 虚拟地址范围的 level 0 页表中的条目不能同时有效。

当 64 KB 页表项所涵盖的分配被放置到大小为 64 KB 的内存段时，64 KB 页表项将变为无效，并且对应的 4 KB 页表项将变为有效。

在下图中，有 4 KB 分配，64 KB 的分配与 level0 页表和支持 64 KB 页的段中所涵盖的相同虚拟地址范围。

![双 pte 模式页表](images/support-for-64kb-pages.1.png)

 

 





