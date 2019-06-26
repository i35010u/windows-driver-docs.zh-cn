---
title: PoolMon 显示
description: PoolMon 显示
ms.assetid: 1dee4331-a508-4e7f-b621-4d22f6572aec
keywords:
- PoolMon WDK 显示
- 内存池监视器 WDK，显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea1ee90c780bf56cb1e202b3f4b749c233157e63
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358271"
---
# <a name="poolmon-display"></a>PoolMon 显示

Poolmon 可在命令窗口中显示有关池的内存分配数据的列。 使用箭头键、 PAGE UP 和 PAGE DOWN 键滚动浏览数据。

>[!NOTE]
>若要查看整个 PoolMon 显示，命令提示符窗口大小必须为至少 80 个字符宽 (宽度 = 80) 和高至少 53 行 (高度 = 53);和命令提示符窗口缓冲区必须至少 500 个字符宽 (宽度 = 500) 和高至少 2000年行 (高度 = 2000年)。 否则，显示可能会被截断。

下表介绍 PoolMon 显示中的列。

|列名称|描述|
|----|----|
|**Tag**|4 字节标记分配给池分配。|
|**Type**|内存分配是否在分页或非分页字节数。|
|**分配**|分配数。|
|**( )**|自上次更新后的分配数中的变化。|
|**释放**|可用操作的数目。|
|**( )**|自上次更新后的分配数中的变化。|
|**Diff**|可用操作的数量减的分配数。|
|**字节数**|以字节为单位使用的分配的大小。|
|**( )**|自上次更新后的分配大小变化。|
|**每个分配**|值的字节数除以的值的比较。|
|**Mapped_Driver**|本地驱动程序 ( **/c**) 和其他常用的驱动程序和系统组件 ( **/g**) 分配的池标记值。 会显示此列，只能使用 **/c**或 **/g**参数。|

以下示例 PoolMon 输出按分配数。 (若要排序你显示这种方式，请启动与 PoolMon **/a**参数。)

```command
 Memory:  260620K Avail:   96364K  PageFlts:     0   InRam Krnl: 1916K P:17856K
 Commit: 203500K Limit: 640916K Peak: 260632K            Pool N: 8332K P:27220K
 System pool information
 Tag  Type     Allocs            Frees            Diff   Bytes       Per Alloc

 Wait Nonp    3971107 (   0)   3971077 (   0)       30    8456 (     0)    281
 ObSt Nonp    2791258 (   0)   2791258 (   0)        0       0 (     0)      0
 Gxlt Paged   1161638 (   0)   1161630 (   0)        8     864 (     0)    108
 Ustm Paged   1088342 (   0)   1088298 (   0)       44    2464 (     0)     56
 Io   Nonp    1021112 (   1)   1020985 (   1)      127   91912 (     0)    723
 ObSq Paged    967615 (   0)    967615 (   0)        0       0 (     0)      0
 Key  Paged    954821 (   0)    953979 (   0)      842   87528 (     0)    103
 SePa Nonp     680348 (   0)    680321 (   0)       27    3656 (     0)    135
```

## <a name="update-rate"></a>更新的速率

PoolMon 更新其显示每隔 5 秒。 您不能以编程方式更改的更新频率。 如果 PoolMon 运行中的窗口具有焦点，但是，可以通过单击一些键，强制 PoolMon 结果的刷新。 **CTRL**并**ALT**，例如，强制进行刷新; 但是，**打印屏幕**却没有。

## <a name="accumulated-values"></a>累计的值

Poolmon 可显示的数据是收集和计算的 Windows，只要启用了池标记。 分配、 可用操作和使用字节数的值所经历的 Windows 启动时，会累积并单调增加，直到重新启动 Windows。 如果驱动程序或组件已启动已启动 Windows 后，从驱动程序或组件启动和重置仅当驱动程序或系统重新启动时的最后一个时间聚合值。

## <a name="interpreting-tag-values"></a>解释标记值

所有池内存分配都有标记，但是它们却不是所有特性的标记值。 池分配具有特性标记的值时分配的内存的驱动程序使用设置标记值的内存[ **ExAllocatePoolWithTag** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)或[ **ExAllocatePoolWithQuotaTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithquotatag)。 如果该驱动程序不会分配某个标记值 ([**ExAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepool)， [ **ExAllocatePoolWithQuota**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithquota))，Windows 仍会创建一个标记，但它无分配默认标记值。 因此，无法区分从其他池分配的该驱动程序分配的统计信息。
