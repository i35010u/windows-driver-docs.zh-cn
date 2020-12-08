---
title: address
description: 地址扩展显示有关目标进程或目标计算机使用的内存的信息。
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
ms.openlocfilehash: dc3284a0ecbc9e84321cf52e4d67b9f258802497
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800151"
---
# <a name="address"></a>!address


**！ Address** extension 显示了有关目标进程或目标计算机使用的内存的信息。

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

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
仅显示包含 *地址* 的地址空间区域。

<span id="_______-summary______"></span><span id="_______-SUMMARY______"></span>**-摘要**   
仅显示摘要信息。

<span id="_______-f_F1__F2__..."></span><span id="_______-f_f1__f2__..."></span><span id="_______-F_F1__F2__..."></span>**-f**：*F1*、 *F2*.。。  
仅显示筛选器 *F1*、 *F2* 等指定的区域。

以下筛选器值按目标进程使用的方式指定内存区域。

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
<td align="left"><p>繁忙区域。 这些区域包括所有虚拟分配块、SBH 堆、自定义分配器的内存，以及不属于任何其他分类的地址空间的所有其他区域。</p></td>
</tr>
<tr class="even">
<td align="left"><p>免费</p></td>
<td align="left"><p>可用内存。 这包括尚未保留的所有内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>映像</p></td>
<td align="left"><p>映射到作为可执行映像的一部分的文件的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>堆栈</p></td>
<td align="left"><p>用于线程堆栈的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Teb</p></td>
<td align="left"><p>用于线程环境的内存块 (TEBs) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Peb</p></td>
<td align="left"><p>用于进程环境的内存块 (PEB) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>堆</p></td>
<td align="left"><p>用于堆的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PageHeap</p></td>
<td align="left"><p>用于整页堆的内存区域。</p></td>
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
<td align="left"><p> (NLS) 表所用的国家/地区语言支持的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FileMap</p></td>
<td align="left"><p>内存映射文件所用的内存。 此筛选器仅适用于实时调试。</p></td>
</tr>
</tbody>
</table>

 

以下筛选器值按内存类型指定内存区域。

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
<td align="left"><p>映射到作为可执行映像的一部分的文件的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MEM_MAPPED</p></td>
<td align="left"><p>映射到不属于可执行映像的文件的内存。 这包括映射到页面文件的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MEM_PRIVATE</p></td>
<td align="left"><p>专用内存。 此内存不会由任何其他进程共享，并且不会映射到任何文件。</p></td>
</tr>
</tbody>
</table>

 

以下筛选器值按内存状态指定内存区域。

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
<td align="left"><p>可用内存。 这包括尚未保留的所有内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MEM_RESERVE</p></td>
<td align="left"><p>保留内存。</p></td>
</tr>
</tbody>
</table>

 

以下筛选器值通过应用于内存的保护来指定内存区域。

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
<td align="left"><p>无法访问的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PAGE_READONLY</p></td>
<td align="left"><p>可读但不可写入且不可执行的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PAGE_READWRITE</p></td>
<td align="left"><p>可读和可写但不可执行的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PAGE_WRITECOPY</p></td>
<td align="left"><p>具有写入时复制行为的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PAGE_EXECUTE</p></td>
<td align="left"><p>可执行，但不可读且不可写入的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PAGE_EXECUTE_READ</p></td>
<td align="left"><p>可执行且可读但不可写入的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PAGE_EXECUTE_READWRITE</p></td>
<td align="left"><p>可执行、可读和可写的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PAGE_EXECUTE_WRITECOPY</p></td>
<td align="left"><p>可执行且具有写入时复制行为的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PAGE_GUARD</p></td>
<td align="left"><p>用作保护页的内存。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PAGE_NOCACHE</p></td>
<td align="left"><p>未缓存的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PAGE_WRITECOMBINE</p></td>
<td align="left"><p>启用了写入合并访问的内存。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-o__csv___tsv___1_"></span><span id="_______-O__CSV___TSV___1_"></span>**-o：**{**csv**  |  **tsv**  |  **1**}  
根据以下选项之一显示输出。

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
<td align="left"><p>将输出显示为逗号分隔值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>tsv</p></td>
<td align="left"><p>将输出显示为制表符分隔值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>以简略格式显示输出。 使用 <strong>！ address</strong> 作为 <strong><a href="-foreach.md" data-raw-source="[.foreach](-foreach.md)">foreach</a></strong>的输入时，此格式很有用。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-c__Command_"></span><span id="_______-c__command_"></span><span id="_______-C__COMMAND_"></span>**-c**： "*Command*"  
为每个内存区域执行自定义命令。 你可以在命令中使用以下占位符来表示 **！地址** 扩展的输出字段。

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
<td align="left"><p>类型</p></td>
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
<td align="left"><p>使用情况</p></td>
</tr>
</tbody>
</table>

 

例如， `!address -f:Heap -c:".echo %1 %3 %5"` 显示类型 **堆** 的每个内存区域的基址、大小和状态。

命令中的引号前面必须加上反斜杠 (\\ ") 。 例如，！ f:Heap-c： "s-a %1 %2 \\ " pad \\ "" 搜索类型 **堆** 的每个内存区域中的字符串 "pad"。

不支持用分号分隔的多个命令。

<span id="_______-_______"></span> **-?**   
在 [调试器命令窗口](debugger-command-window.md)中显示此扩展的最小帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何显示和搜索内存的详细信息，请参阅 [读取和写入内存](reading-and-writing-memory.md)。 有关显示内存属性的其他扩展，请参阅 [**！ vm**](-vm.md) (内核模式) 和 [**！ vprot**](-vprot.md) (用户模式) 。

<a name="remarks"></a>备注
-------

如果没有任何参数， **！地址** 扩展将显示有关整个地址空间的信息。 **！ Address-summary** 命令仅显示摘要。

在内核模式下，即使使用了，此扩展也只搜索核心内存 [**。处理 (设置进程上下文)**](-process--set-process-context-.md) 来指定给定进程的虚拟地址空间。 在用户模式下， **！地址** 扩展始终指目标进程拥有的内存。

在用户模式下， **！地址***地址* 显示指定地址所属区域的特征。 如果没有参数， **！ address** 将显示所有内存区域的特征。 这些特征包括内存使用情况、内存类型、内存状态和内存保护。 有关此信息的含义的详细信息，请参阅 **-f** 参数说明中前面的表。

下面的示例使用 **！ address** 检索有关映射到 kernel32.dll 的内存区域的信息。

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

此示例使用 *Address* 值0x75831234。 此显示显示此地址位于以地址0x75831000 开头的内存区域中，并以地址0x758f6000 结束。 区域具有使用情况 **图像**、类型 **mem \_ 映像**、状态 **内存 \_ 提交** 和保护 **页 \_ 执行 \_ 读取**。  (有关这些值的含义的详细信息，请参阅前面的表。 ) 显示还会列出三个其他调试程序命令，你可以使用这些命令来获取有关此内存地址的详细信息。

如果是从地址开始，并尝试确定其相关信息，则使用情况信息通常是最有价值的。 了解用法后，可以使用其他扩展来了解有关此内存的详细信息。 例如，如果使用是 **堆**，则可以使用 [**！堆**](-heap.md) 扩展来了解详细信息。

下面的示例使用 [**s (Search Memory)**](s--search-memory-.md) 命令在类型为 **Image** 的每个内存区域中搜索宽字符字符串 "Note"。

```console
!address /f:Image /c:"s -u %1 %2 \"Note\""

**_ Executing: s -u 0xab0000 0xab1000 "Note"
_*_ Executing: s -u 0xab1000 0xabc000 "Note"
00ab2936  004e 006f 0074 0065 0070 0061 0064 0000  N.o.t.e.p.a.d...
00ab2f86  004e 006f 0074 0065 0070 0061 0064 005c  N.o.t.e.p.a.d.\.
00ab32e4  004e 006f 0074 0065 0070 0061 0064 0000  N.o.t.e.p.a.d...
_*_ Executing: s -u 0xabc000 0xabd000 "Note"
. . .
```

在内核模式下，_ *！ address** 的输出类似于用户模式输出，但包含的信息更少。 下面的示例演示内核模式输出。

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

"使用情况" 的含义与在用户模式下的含义相同。 "ImageName" 指示与该地址关联的模块。 "KernelStack" 显示此线程的 ETHREAD 块 (0x817B4DA0) 、进程 ID (0x324) 和线程 ID (0x368) 的地址。

 

 





