---
title: PoolMon 显示
description: PoolMon 显示
ms.assetid: 1dee4331-a508-4e7f-b621-4d22f6572aec
keywords:
- PoolMon WDK 显示
- 内存池监视器 WDK，显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5171528fd8506c333c02338b5b4144d037778489
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568198"
---
# <a name="poolmon-display"></a>PoolMon 显示


## <span id="ddk_poolmon_display_tools"></span><span id="DDK_POOLMON_DISPLAY_TOOLS"></span>


Poolmon 可在命令窗口中显示有关池的内存分配数据的列。 使用箭头键、 PAGE UP 和 PAGE DOWN 键滚动浏览数据。

**请注意**  若要查看整个 PoolMon 显示，命令提示符窗口大小必须为至少 80 个字符宽 (宽度 = 80) 和高至少 53 行 (高度 = 53); 和命令提示符窗口缓冲区必须至少 500 个字符宽 （宽度= 500） 和高至少 2000年行 (高度 = 2000年)。 否则，显示可能会被截断。

 

下表介绍 PoolMon 显示中的列。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">列名称</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Tag</strong></p></td>
<td align="left"><p>4 字节标记分配给池分配。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Type</strong></p></td>
<td align="left"><p>内存分配是否在分页或非分页字节数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>分配</strong></p></td>
<td align="left"><p>分配数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>( )</strong></p></td>
<td align="left"><p>自上次更新后的分配数中的变化。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>释放</strong></p></td>
<td align="left"><p>可用操作的数目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>( )</strong></p></td>
<td align="left"><p>自上次更新后的分配数中的变化。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Diff</strong></p></td>
<td align="left"><p>可用操作的数量减的分配数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>字节数</strong></p></td>
<td align="left"><p>以字节为单位使用的分配的大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>( )</strong></p></td>
<td align="left"><p>自上次更新后的分配大小变化。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>每个分配</strong></p></td>
<td align="left"><p>值的字节数除以的值的比较。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Mapped_Driver</strong></p></td>
<td align="left"><p>本地驱动程序 (<strong>/c</strong>) 和其他常用的驱动程序和系统组件 (<strong>/g</strong>) 分配的池标记值。 会显示此列，只能使用<strong>/c</strong>或<strong>/g</strong>参数。</p></td>
</tr>
</tbody>
</table>

 

以下示例 PoolMon 输出按分配数。 (若要排序你显示这种方式，请启动与 PoolMon **/a**参数。)

```
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

### <a name="span-idupdateratespanspan-idupdateratespanspan-idupdateratespanupdate-rate"></a><span id="Update_Rate"></span><span id="update_rate"></span><span id="UPDATE_RATE"></span>更新的速率

PoolMon 更新其显示每隔 5 秒。 不能更改的更新频率。

### <a name="span-idaccumulatedvaluesspanspan-idaccumulatedvaluesspanspan-idaccumulatedvaluesspanaccumulated-values"></a><span id="Accumulated_Values"></span><span id="accumulated_values"></span><span id="ACCUMULATED_VALUES"></span>累计的值

Poolmon 可显示的数据是收集和计算的 Windows，只要启用了池标记。 分配、 可用操作和使用字节数的值所经历的 Windows 启动时，会累积并单调增加，直到重新启动 Windows。 如果驱动程序或组件已启动已启动 Windows 后，从驱动程序或组件启动和重置仅当驱动程序或系统重新启动时的最后一个时间聚合值。

### <a name="span-idinterpretingtagvaluesspanspan-idinterpretingtagvaluesspanspan-idinterpretingtagvaluesspaninterpreting-tag-values"></a><span id="Interpreting_Tag_Values"></span><span id="interpreting_tag_values"></span><span id="INTERPRETING_TAG_VALUES"></span>解释标记值

所有池内存分配都有标记，但是它们却不是所有特性的标记值。 池分配具有特性标记的值时分配的内存的驱动程序使用设置标记值的内存[ **ExAllocatePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544520)或[ **ExAllocatePoolWithQuotaTag**](https://msdn.microsoft.com/library/windows/hardware/ff544513)。 如果该驱动程序不会分配某个标记值 ([**ExAllocatePool**](https://msdn.microsoft.com/library/windows/hardware/ff544501)， [ **ExAllocatePoolWithQuota**](https://msdn.microsoft.com/library/windows/hardware/ff544506))，Windows 仍会创建一个标记，但它无分配默认标记值。 因此，无法区分从其他池分配的该驱动程序分配的统计信息。

 

 





