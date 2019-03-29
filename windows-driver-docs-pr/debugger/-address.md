---
title: 地址
description: 地址扩展显示目标进程或目标计算机使用的内存有关的信息。
ms.assetid: 9bbde680-8523-4db2-bb7e-fdacdaf1aa89
keywords:
- 解决 Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- address
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 701a0090477587111490061f66f6217477f700d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564364"
---
# <a name="address"></a>!address


**！ 地址**扩展显示目标进程或目标计算机使用的内存有关的信息。

User-Mode

```dbgcmd
!address Address
!address -summary 
!address [-f:F1,F2,...] {[-o:{csv | tsv | 1}] | [-c:"Command"]}
!address -? | -help
```

Kernel-Mode

```dbgcmd
!address Address 
!address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
显示仅包含的地址空间的区域*地址*。

<span id="_______-summary______"></span><span id="_______-SUMMARY______"></span> **-summary**   
仅显示摘要信息。

<span id="_______-f_F1__F2__..."></span><span id="_______-f_f1__f2__..."></span><span id="_______-F_F1__F2__..."></span> **-f**:*F1*， *F2*，...  
显示筛选器指定的区域*F1*， *F2*，依次类推。

以下筛选器值的目标进程正在使用它们的方式指定内存区域。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">筛选器值</th>
<th align="left">显示的内存区域</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>VAR</p></td>
<td align="left"><p>繁忙的区域。 这些区域包括所有虚拟分配块、 SBH 堆、 从自定义分配器的内存和其他的所有区域的地址空间分为无其他分类。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Free</p></td>
<td align="left"><p>可用内存。 这包括所有未保留的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>图像</p></td>
<td align="left"><p>映射到可执行映像的一部分的文件的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>堆栈</p></td>
<td align="left"><p>用于线程堆栈的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>teb</p></td>
<td align="left"><p>用于线程环境块 (Teb) 的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Peb</p></td>
<td align="left"><p>使用进程环境块 (PEB) 内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>堆</p></td>
<td align="left"><p>使用的堆内存量。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PageHeap</p></td>
<td align="left"><p>用于在整页堆的内存区域。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CSR</p></td>
<td align="left"><p>CSR 共享内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Actx</p></td>
<td align="left"><p>用于激活上下文数据的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>NLS</p></td>
<td align="left"><p>用于区域语言支持 (NLS) 的表的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FileMap</p></td>
<td align="left"><p>内存映射文件使用的内存。 此筛选器仅在实时调试过程才适用。</p></td>
</tr>
</tbody>
</table>

 

以下筛选器值指定内存类型的内存的区域。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">筛选器值</th>
<th align="left">显示的内存区域</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>MEM_IMAGE</p></td>
<td align="left"><p>映射到可执行映像的一部分的文件的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MEM_MAPPED</p></td>
<td align="left"><p>映射到不是可执行映像的一部分的文件的内存。 这包括映射到分页文件的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MEM_PRIVATE</p></td>
<td align="left"><p>专用内存。 此内存不共享任何其他进程和未映射到任何文件。</p></td>
</tr>
</tbody>
</table>

 

以下筛选器值的内存状态的指定内存区域。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">筛选器值</th>
<th align="left">显示的内存区域</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>MEM_COMMIT</p></td>
<td align="left"><p>提交的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MEM_FREE</p></td>
<td align="left"><p>可用内存。 这包括所有未保留的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MEM_RESERVE</p></td>
<td align="left"><p>保留的内存。</p></td>
</tr>
</tbody>
</table>

 

以下筛选器值应用于内存的保护通过指定内存区域。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">筛选器值</th>
<th align="left">显示的内存区域</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>PAGE_NOACCESS</p></td>
<td align="left"><p>不能访问的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PAGE_READONLY</p></td>
<td align="left"><p>是可读，但不可写且非可执行的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PAGE_READWRITE</p></td>
<td align="left"><p>是可读和可写的但非可执行的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PAGE_WRITECOPY</p></td>
<td align="left"><p>已写入时复制行为的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PAGE_EXECUTE</p></td>
<td align="left"><p>是可执行文件，但不可读和不可写入的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PAGE_EXECUTE_READ</p></td>
<td align="left"><p>是可执行文件和可读，但不可写的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PAGE_EXECUTE_READWRITE</p></td>
<td align="left"><p>是可执行文件、 可读，并且必须可写内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PAGE_EXECUTE_WRITECOPY</p></td>
<td align="left"><p>它是可执行文件并具有写入时复制行为的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PAGE_GUARD</p></td>
<td align="left"><p>充当一个保护页的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PAGE_NOCACHE</p></td>
<td align="left"><p>未缓存的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PAGE_WRITECOMBINE</p></td>
<td align="left"><p>已启用的写入-将访问的内存。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-o__csv___tsv___1_"></span><span id="_______-O__CSV___TSV___1_"></span> **-o:**{**csv** | **tsv** | **1**}  
显示根据下列选项之一的输出。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">输出格式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>csv</p></td>
<td align="left"><p>以逗号分隔值的形式显示输出。</p></td>
</tr>
<tr class="even">
<td align="left"><p>tsv</p></td>
<td align="left"><p>以制表符分隔值的形式显示输出。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>裸机格式显示输出。 此格式的工作以及当<strong>！ 地址</strong>用作输入 <strong><a href="-foreach.md" data-raw-source="[.foreach](-foreach.md)">.foreach</a></strong>。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-c__Command_"></span><span id="_______-c__command_"></span><span id="_______-C__COMMAND_"></span> **-c**:"*Command*"  
执行每个内存区域的自定义命令。 可以在命令中使用的以下占位符来表示的输出字段 **！ 地址**扩展。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">占位符</th>
<th align="left">输出字段</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>%1</p></td>
<td align="left"><p>基址</p></td>
</tr>
<tr class="even">
<td align="left"><p>%2</p></td>
<td align="left"><p>结束地址 + 1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%3</p></td>
<td align="left"><p>区域大小</p></td>
</tr>
<tr class="even">
<td align="left"><p>%4</p></td>
<td align="left"><p>在任务栏的搜索框中键入</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%5</p></td>
<td align="left"><p>状态</p></td>
</tr>
<tr class="even">
<td align="left"><p>%6</p></td>
<td align="left"><p>保护</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%7</p></td>
<td align="left"><p>用法</p></td>
</tr>
</tbody>
</table>

 

例如，`!address -f:Heap -c:".echo %1 %3 %5"`基址、 大小和类型的每个内存区域的状态将显示**堆**。

在命令中的引号必须加反斜杠 (\\")。 例如，！ 地址-f： 堆-c:"s-a %1 %2 \\"pad\\""中搜索类型的每个内存区域**堆**"板"的字符串。

不支持多个命令之间用分号分隔。

<span id="_______-_______"></span> **-?**   
显示最少的帮助文本中此扩展[调试器命令窗口](debugger-command-window.md)。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关如何显示和搜索内存的详细信息，请参阅[读取和写入内存](reading-and-writing-memory.md)。 显示内存属性的其他扩展，请参阅[ **！ vm** ](-vm.md) （内核模式） 和[ **！ vprot** ](-vprot.md) （用户模式）。

<a name="remarks"></a>备注
-------

不带任何参数， **！ 地址**扩展显示整个地址空间有关的信息。 **！ 地址-摘要**命令仅显示摘要。

在内核模式下，此扩展仅内核在内存中搜索，即使你使用[ **.process （设置进程上下文）** ](-process--set-process-context-.md)指定给定的进程的虚拟地址空间。 在用户模式下 **！ 地址**扩展始终是指目标进程拥有的内存。

在用户模式下 **！ 地址***地址*显示指定的地址所属的区域的特征。 不带参数， **！ 地址**显示所有的内存区域的特征。 这些特征包括内存使用情况、 内存类型、 内存状态和内存保护。 此信息的含义的详细信息，请参阅前面表中的说明 **-f**参数。

下面的示例使用 **！ 地址**来检索有关某个区域的映射到 kernel32.dll 的内存的信息。

```console
0:000> !address 75831234
Usage:                  Image
Base Address:           75831000
End Address:            758f6000
Region Size:            000c5000
Type:                   01000000MEM_IMAGE
State:                  00001000MEM_COMMIT
Protect:                00000020PAGE_EXECUTE_READ
More info:              lmv m kernel32
More info:              !lmi kernel32
More info:              ln 0x75831234
```

此示例使用*地址*0x75831234 的值。 屏幕将显示此地址是与地址 0x75831000 开头和结尾的地址 0x758f6000 的内存区域中。 则区域的使用情况**图像**，类型**内存优化\_图像**，状态**内存优化\_提交**，并保护**页\_执行\_读取**。 （有关这些值的含义的详细信息，请参阅前面的表）。显示还列出了可用于获取有关此内存地址的详细信息的三个其他调试器命令。

如果您是从一个地址并尝试确定有关它的信息，是经常最有价值的使用情况信息。 了解使用情况后，可以使用其他扩展若要了解有关此内存的详细信息。 例如，如果的使用率**堆**，可以使用[ **！ 堆**](-heap.md)扩展，以了解详细信息。

下面的示例使用[ **s （内存搜索）** ](s--search-memory-.md)命令来搜索类型的每个内存区域**图像**对于宽字符的字符串"说明"。

```console
!address /f:Image /c:"s -u %1 %2 \"Note\""

*** Executing: s -u 0xab0000 0xab1000 "Note"
*** Executing: s -u 0xab1000 0xabc000 "Note"
00ab2936  004e 006f 0074 0065 0070 0061 0064 0000  N.o.t.e.p.a.d...
00ab2f86  004e 006f 0074 0065 0070 0061 0064 005c  N.o.t.e.p.a.d.\.
00ab32e4  004e 006f 0074 0065 0070 0061 0064 0000  N.o.t.e.p.a.d...
*** Executing: s -u 0xabc000 0xabd000 "Note"
. . .
```

在内核模式下的输出 **！ 地址**类似于用户模式下输出，但包含较少的信息。 下面的示例显示了内核模式输出。

```console
kd> !address
  804de000 - 00235000                           
 Usage       KernelSpaceUsageImage
          ImageName   ntoskrnl.exe

  80c00000 - 001e1000
          Usage       KernelSpaceUsagePFNDatabase

....

  f85b0000 - 00004000
          Usage       KernelSpaceUsageKernelStack
          KernelStack 817b4da0 : 324.368

 f880d000 - 073d3000
          Usage       KernelSpaceUsageNonPagedPoolExpansion
```

"使用情况"的含义是用户模式相同。 "ImageName"指示与此地址相关联的模块。 "KernelStack"会显示此线程 ETHREAD 块 (0x817B4DA0)、 进程 ID (0x324) 和线程 ID (0x368) 的地址。

 

 





