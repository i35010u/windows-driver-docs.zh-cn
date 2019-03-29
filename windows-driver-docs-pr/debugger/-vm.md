---
title: vm
description: Vm 扩展在目标系统上显示有关虚拟内存使用统计信息的摘要信息。
ms.assetid: 25e4f80c-d4ca-407c-991d-e8ee5dfbb309
keywords:
- 调试 Windows vm
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- vm
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eb4ae55dd673f84744b856e7154b9e8b2b1158c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563570"
---
# <a name="vm"></a>!vm


**！ Vm**扩展目标系统上显示有关虚拟内存使用统计信息的摘要信息。

```dbgcmd
!vm [Flags]
```

## <a name="span-idddkvmdbgspanspan-idddkvmdbgspanparameters"></a><span id="ddk__vm_dbg"></span><span id="DDK__VM_DBG"></span>参数


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定将在此命令的输出中显示哪些信息。 这可以是以下位任何之和。 默认值为 0，这会导致显示以包括系统范围虚拟内存统计信息，以及每个进程的内存统计信息。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
将导致显示效果以省略了特定于进程的统计信息。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
将导致显示以包括内存管理线程堆栈。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
将导致显示以包括终端服务器内存使用情况。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
将导致显示以包括页面文件写入日志。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>4 位 (0x10)  
将导致显示以包括工作集所有者线程堆栈。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>5 位 (0x20)  
(Windows Vista 及更高版本)将导致显示以包括内核虚拟地址使用情况。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

|       |                  |
|-------|------------------|
| 模式 | 内核模式下 |

 

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

[ **！ Memusage** ](-memusage.md)扩展命令可用于分析的物理内存使用情况。 有关内存管理的详细信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

下面是短时，生成的输出的示例*标志*为 1:

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

使用在页与千字节为单位中列出的所有内存。 以下是在此显示中最有用的信息：

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
<td align="left"><p>在系统中的总物理内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>可用的页面</strong></p></td>
<td align="left"><p>可在虚拟和物理系统上的内存页的数目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>非分页缓冲的池使用情况</strong></p></td>
<td align="left"><p>分配给非分页缓冲池的页的量。 非分页的池是内存无法换出到分页文件中，因此它必须始终占用的物理内存。 如果此数字过大，这通常是指示存在为内存泄漏某个位置在系统中。</p></td>
</tr>
</tbody>
</table>

 

 

 





