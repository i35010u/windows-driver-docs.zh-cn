---
title: Vmnetwork
description: Vm 扩展显示有关目标系统上的虚拟内存使用统计信息的摘要信息。
ms.assetid: 25e4f80c-d4ca-407c-991d-e8ee5dfbb309
keywords:
- vm Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- vm
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eaaa9cf742780e9f186c9eded8a13a777d7899f1
ms.sourcegitcommit: 2aa583e3da4ae9338a0d11678bf77f1460286f2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "70025161"
---
# <a name="vm"></a>!vm


**！ Vm**扩展显示有关目标系统上的虚拟内存使用统计信息的摘要信息。

```dbgcmd
!vm [Flags]
```

## <a name="span-idddk__vm_dbgspanspan-idddk__vm_dbgspanparameters"></a><span id="ddk__vm_dbg"></span><span id="DDK__VM_DBG"></span>Parameters


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定将在此命令的输出中显示的信息。 这可以是以下位的任意总和。 默认值为0，这将导致显示包含系统范围内的虚拟内存统计信息，以及每个进程的内存统计信息。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位0（0x1）  
使显示忽略特定于进程的统计信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位1（0x2）  
使显示包含内存管理线程堆栈。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位2（0x4）  
使显示包含终端服务器内存使用量。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位3（0x8）  
导致显示包含页面文件写入日志。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位4（0x10）  
使显示包含工作集所有者线程堆栈。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>位5（0x20）  
（Windows Vista 和更高版本）导致显示包含内核虚拟地址使用情况。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

|       |                  |
|-------|------------------|
| 交货 | 仅限内核模式 |

 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p>Kdexts</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

[ **！ Memusage**](-memusage.md) extension 命令可用于分析物理内存使用情况。 有关内存管理的详细信息，请参阅 Russinovich 和 David 所罗门群岛的*Microsoft Windows 内部机制*。

<a name="remarks"></a>备注
-------

下面是在*Flags*为1时生成的短输出的示例：

```dbgcmd
kd> !vm 1

*** Virtual Memory Usage ***
      Physical Memory:     16270   (   65080 Kb)
      Page File: \??\E:\pagefile.sys
         Current:     98304Kb Free Space:     61044Kb
 Minimum:     98304Kb Maximum:       196608Kb
      Available Pages:      5543   (   22172 Kb)
      ResAvail Pages:       6759   (   27036 Kb)
      Locked IO Pages:       112   (     448 Kb)
 Free System PTEs:    45089   (  180356 Kb)
      Free NP PTEs:         5145   (   20580 Kb)
      Free Special NP:       336   (    1344 Kb)
      Modified Pages:        714   (    2856 Kb)
      NonPagedPool Usage:    877   (    3508 Kb)
      NonPagedPool Max:     6252   (   25008 Kb)
      PagedPool 0 Usage:     729   (    2916 Kb)
      PagedPool 1 Usage:     432   (    1728 Kb)
      PagedPool 2 Usage:     436   (    1744 Kb)
      PagedPool Usage:      1597   (    6388 Kb)
      PagedPool Maximum:   13312   (   53248 Kb)
      Shared Commit:        1097   (    4388 Kb)
      Special Pool:          229   (     916 Kb)
      Shared Process:       1956   (    7824 Kb)
      PagedPool Commit:     1597   (    6388 Kb)
      Driver Commit:         828   (    3312 Kb)
      Committed pages:     21949   (   87796 Kb)
      Commit limit:        36256   (  145024 Kb)
```

所有内存使用情况都在页中列出，以 kb 为单位。 此显示中最有用的信息如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>物理内存</strong></p></td>
<td align="left"><p>系统中的总物理内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>可用页面</strong></p></td>
<td align="left"><p>系统上可用的内存页数（虚拟机和物理内存）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>非分页池使用情况</strong></p></td>
<td align="left"><p>分配给非分页池的页数。 非分页池是无法换出到页面文件的内存，因此它必须始终占用物理内存。 如果此数字过大，则这通常表示系统中某个位置存在内存泄漏。</p></td>
</tr>
</tbody>
</table>

 

 

 





