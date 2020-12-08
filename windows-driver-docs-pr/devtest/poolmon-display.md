---
title: PoolMon 显示
description: PoolMon 显示
keywords:
- PoolMon WDK，显示
- 内存池监视器 WDK，显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a54a2327068a38d383efa017c070d44110976635
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841019"
---
# <a name="poolmon-display"></a>PoolMon 显示

PoolMon 在命令窗口中显示有关池内存分配的数据的列。 使用箭头键、PAGE UP 和 PAGE DOWN 键滚动查看数据。

>[!NOTE]
>若要查看整个 PoolMon 显示，命令提示符窗口的大小必须至少为80个字符宽 (width = 80) ，至少53行高 (高度 = 53) ;并且命令提示符窗口缓冲区的宽度必须至少为500个字符 (width = 500) ，至少2000行高 (height = 2000) 。 否则，显示可能会被截断。

下表描述了 PoolMon 显示中的列。

|列名|描述|
|----|----|
|**标记**|分配给池分配的4字节标记。|
|**类型**|内存分配是否处于分页或非分页字节。|
|**Allocs**|分配数。|
|**( )**|自上次更新以来的分配数的变化。|
|**释放**|可用操作的数量。|
|**( )**|自上次更新以来的分配数的变化。|
|**差异**|分配数减去可用操作的数量。|
|**字节**|分配的大小（以字节为单位）。|
|**( )**|自上次更新以来分配的大小变化。|
|**按分配**|Bytes 的值除以 Diff 的值。|
|**Mapped_Driver**|本地驱动程序 (**/c**) 和其他常用的驱动程序和系统组件 (**/g**) 分配池标记值。 仅当使用 **/c** 或 **/g** 参数时，才会显示此列。|

下面的示例 PoolMon 输出按分配数进行排序。  (以这种方式对您的显示进行排序，请用 **/a** 参数开始 PoolMon。 ) 

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

## <a name="update-rate"></a>更新速率

PoolMon 每5秒钟更新一次。 不能以编程方式更改更新速率。 但是，如果在中运行的 windows PoolMon 有焦点，则可以通过单击某些键来强制刷新 PoolMon 结果。 例如，按 **CTRL** 和 **ALT**; 强制刷新;不过，**打印屏幕** 却不能。

## <a name="accumulated-values"></a>累计值

如果启用了池标记，则由 Windows 收集和计算 PoolMon 显示的数据。 分配的值、可用操作和使用的字节数从 Windows 启动时开始，并在 Windows 重新启动之前递增。 如果在 Windows 启动之后启动驱动程序或组件，则将从上次启动驱动程序或组件时开始的时间开始，并在驱动程序或系统重新启动时将其重置。

## <a name="interpreting-tag-values"></a>解释标记值

所有池内存分配都有标记，但是它们并非都具有特征标记值。 当分配内存的驱动程序使用 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 或 [**ExAllocatePoolWithQuotaTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag)设置标记值时，池内存分配具有特征标记值。 如果驱动程序没有分配标记值 ([**ExAllocatePool**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool)， [**ExAllocatePoolWithQuota**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquota)) ，则 Windows 仍会创建一个标记，但会将默认标记值指定为 None。 因此，不能将该驱动程序的分配的统计信息与其他池分配的统计信息区分开来。
