---
title: 堆栈
description: 堆扩展显示堆使用情况信息，控制堆管理器中的断点，检测泄漏的堆块，搜索堆块，或显示页堆信息。
ms.assetid: 70947b56-1a8c-4e78-85d0-d5df87f3150c
keywords:
- 堆使用情况
- GFlags，启用页堆
- 堆窗口调试
ms.date: 08/23/2019
topic_type:
- apiref
api_name:
- heap
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8b10538ea1a4de33199b59796deb8d1e9265a452
ms.sourcegitcommit: 0610366df5de756bf8aa6bfc631eba5e3cd84578
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2019
ms.locfileid: "72021054"
---
# <a name="heap"></a>!heap


**！堆**扩展显示堆使用情况信息，控制堆管理器中的断点，检测泄漏的堆块，搜索堆块，或显示页堆信息。

此扩展插件支持段堆和 NT 堆。 Use！没有参数的堆来列出所有堆及其类型。

```dbgcmd
!heap [HeapOptions] [ValidationOptions] [Heap] 
!heap -b [{alloc|realloc|free} [Tag]] [Heap | BreakAddress] 
!heap -B {alloc|realloc|free} [Heap | BreakAddress] 
!heap -l 
!heap -s [SummaryOptions] [StatHeapAddress] 
!heap -i HeapAddress
!heap -x [-v] Address 
!heap -p [PageHeapOptions] 
!heap -srch [Size] Pattern
!heap -flt FilterOptions
!heap -stat [-h Handle [-grp GroupBy [MaxDisplay]]]
!heap [-p] -?
!heap -triage [Handle | Address] 
```

## <a name="span-idsegment_and_nt_heap_parametersspanspan-idsegment_and_nt_heap_parametersspanspan-idsegment_and_nt_heap_parametersspansegment-and-nt-heap-parameters"></a><span id="Segment_and_NT_Heap_Parameters"></span><span id="segment_and_nt_heap_parameters"></span><span id="SEGMENT_AND_NT_HEAP_PARAMETERS"></span>段和 NT 堆参数


这些参数适用于段和 NT 堆。

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**@no__t  
指定正在请求摘要信息。 如果省略了*SummaryOptions*和*StatHeapAddress* ，则将显示与当前进程关联的所有堆的摘要信息。

<span id="_______SummaryOptions______"></span><span id="_______summaryoptions______"></span><span id="_______SUMMARYOPTIONS______"></span>*SummaryOptions*   
可以是下列选项的任意组合。 *SummaryOptions*不区分大小写。 类型！堆-？ 获取其他信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-v</strong></p></td>
<td align="left"><p>验证所有数据块。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-b</strong> <em>BucketSize</em></p></td>
<td align="left"><p>指定存储桶大小。 默认值为1024位。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-d</strong> <em>DumpBlockSize</em></p></td>
<td align="left"><p>指定存储桶大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-a</strong></p></td>
<td align="left"><p>转储所有堆块。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-c</strong></p></td>
<td align="left"><p>指定应显示每个块的内容。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-triage__Handle___Address___"></span><span id="_______-triage__handle___address___"></span><span id="_______-TRIAGE__HANDLE___ADDRESS___"></span> **-会审 \[** <em>句柄</em> **|** <em>地址</em>**0**1  
使调试器自动搜索进程堆中的失败。 如果将堆句柄指定为参数，则将检查该堆;否则，会搜索包含给定地址的所有堆，如果找到，将检查该地址。 使用 **-会审**是验证低碎片堆（LFH）损坏的唯一方法。

<span id="_______-x_-v_"></span><span id="_______-X_-V_"></span> **-x** @no__t **-@no__t-** 5   
使调试器搜索包含指定地址的堆块。 如果添加了-v，则该命令将在当前进程的整个虚拟内存空间中搜索指向此堆块的指针。

<span id="_______-l______"></span><span id="_______-L______"></span> **-l**   
使调试器检测泄漏的堆块。

<span id="_______-i________Address______-h_HeapAddress______"></span><span id="_______-i________address______-h_heapaddress______"></span><span id="_______-I________ADDRESS______-H_HEAPADDRESS______"></span> **-i** *Address* **-h** *HeapAddress*   
显示有关指定*堆*的信息。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*Address*@no__t  
指定要搜索的地址。

<span id="_______-_______"></span> **-?**    
在调试器命令窗口中显示此扩展的一些简短帮助文本。 使用 **！堆-？** 对于常规帮助和 **！堆-p-？** 用于页堆帮助。

## <a name="span-idddk__heap_dbgspanspan-idddk__heap_dbgspannt-heap-parameters"></a><span id="ddk__heap_dbg"></span><span id="DDK__HEAP_DBG"></span>NT 堆参数


这些参数仅适用于 NT 堆。

<span id="_______HeapOptions______"></span><span id="_______heapoptions______"></span><span id="_______HEAPOPTIONS______"></span>*HeapOptions*   
可以是下列选项的任意组合。 *HeapOptions*值区分大小写。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-v</strong></p></td>
<td align="left"><p>使调试器验证指定的堆。</p>
<div class="alert">
<strong>Note @ no__t-1 @ no__t-2This 选项未检测到低碎片堆（LFH）损坏。 改用<strong>-会审</strong>。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-a</strong></p></td>
<td align="left"><p>使显示包含指定堆的所有信息。 大小，在本例中，将向上舍入到堆粒度。 （运行<strong>！</strong>具有<strong>-a</strong>选项的堆等效于使用三个选项<strong>-h-f-m</strong>运行它，这可能需要很长时间。）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-h</strong></p></td>
<td align="left"><p>使显示包含指定堆的所有非 LFH 条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-hl</strong></p></td>
<td align="left"><p>使显示包含指定堆的所有条目，包括 LFH 条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-f</strong></p></td>
<td align="left"><p>使显示包含指定堆的所有可用列表项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-m</strong></p></td>
<td align="left"><p>使显示内容包括指定堆的所有段条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-t</strong></p></td>
<td align="left"><p>使显示包含指定堆的标记信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-T</strong></p></td>
<td align="left"><p>使显示包含指定堆的伪标记条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-g</strong></p></td>
<td align="left"><p>使显示内容包含全局标记信息。 全局标记与每个未标记的分配相关联。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-s</strong></p></td>
<td align="left"><p>使显示内容包括指定堆的摘要信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-k</strong></p></td>
<td align="left"><p>（仅限基于 x86 的目标）使显示内容包括与每个条目关联的 stack backtrace。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______ValidationOptions______"></span><span id="_______validationoptions______"></span><span id="_______VALIDATIONOPTIONS______"></span>*ValidationOptions*   
可以是以下选项中的任何一个。 *ValidationOptions*区分大小写。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-D</strong></p></td>
<td align="left"><p>对指定的堆禁用调用验证。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-E</strong></p></td>
<td align="left"><p>为指定的堆启用调用时验证。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-d</strong></p></td>
<td align="left"><p>为指定的堆禁用堆检查。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-e</strong></p></td>
<td align="left"><p>为指定的堆启用堆检查。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-i________Heap_Address______or_HeapAddress______"></span><span id="_______-i________heap_address______or_heapaddress______"></span><span id="_______-I________HEAP_ADDRESS______OR_HEAPADDRESS______"></span> **-i** *堆* *地址***或** *HeapAddress*   
显示有关指定*堆*的信息。

<span id="_______BreakAddress______"></span><span id="_______breakaddress______"></span><span id="_______BREAKADDRESS______"></span>*BreakAddress*   
指定要在其中设置或删除断点的块的地址。

<span id="_______-b______"></span><span id="_______-B______"></span> **-b**   
使调试器在堆管理器中创建条件断点。 **-B**选项后可以后跟**分配**、 **realloc**或**可用**;这指定是否将通过分配、重新分配或释放内存来激活断点。 如果使用*BreakAddress*来指定块的地址，则可以省略断点类型。 如果使用*堆*指定堆地址或堆索引，则必须包含类型以及*标记*参数。

<span id="_______Tag______"></span><span id="_______tag______"></span><span id="_______TAG______"></span>*标记*   
指定堆中的标记名称。

<span id="_______-B______"></span><span id="_______-b______"></span> **-B**   
使调试器从堆管理器中删除条件断点。 必须指定断点类型（**分配**、 **realloc**或**free**），并且必须与与 **-b**选项一起使用。

<span id="_______StatHeapAddress______"></span><span id="_______statheapaddress______"></span><span id="_______STATHEAPADDRESS______"></span>*StatHeapAddress*   
指定堆的地址。 如果此为0或省略，则显示与当前进程关联的所有堆。

<span id="_______-p______"></span><span id="_______-P______"></span> **-p**   
指定正在请求页堆信息。 如果在没有任何*PageHeapOptions*的情况下使用，则将显示所有页堆。

<span id="_______PageHeapOptions______"></span><span id="_______pageheapoptions______"></span><span id="_______PAGEHEAPOPTIONS______"></span>*PageHeapOptions*   
可以是以下选项中的任何一个。 *PageHeapOptions*区分大小写。 如果未指定任何选项，则将显示所有可能的页堆句柄。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-h</strong> <em>句柄</em></p></td>
<td align="left"><p>使调试器显示有关带有句柄<em>句柄</em>的页堆的详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-a</strong> <em>地址</em></p></td>
<td align="left"><p>使调试器查找其块包含<em>地址</em>的页堆。 将包括此地址如何包含到整页堆块的完整详细信息，如此地址是否是页面堆的一部分、其在块内的偏移量，以及是分配块还是释放块。 每次提供堆栈跟踪。 使用此选项时，大小以堆分配粒度的倍数显示。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-t</strong>[<strong>c</strong>|<strong>s</strong>] [<em>跟踪</em>]</p></td>
<td align="left"><p>使调试器显示大量堆用户的已收集跟踪。 <em>跟踪</em>指定要显示的跟踪数;默认值为四。 如果跟踪超过指定的数量，则显示最早的跟踪。 如果使用<strong>-t</strong>或<strong>-tc</strong> ，则跟踪按计数使用情况进行排序。 如果使用<strong>-ts</strong> ，则跟踪按大小排序。 （仅 Windows XP 支持<strong>-tc</strong>和<strong>-ts</strong>选项; 仅在 windows xp 和更早版本的 windows 中支持<strong>-t</strong>选项。）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-fi</strong> [<em>跟踪</em>]</p></td>
<td align="left"><p>使调试器显示最新的错误注入跟踪。 <em>跟踪</em>指定要显示的数量;默认值为4。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-所有</strong></p></td>
<td align="left"><p>使调试器显示有关所有页堆的详细信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-?</strong></p></td>
<td align="left"><p>使调试器显示页堆帮助，包括堆块的关系图。 （也可以在下面的 "备注" 部分中查看这些关系图。）</p></td>
</tr>
</tbody>
</table>

 

在可以使用 any **！堆-p** extension 命令之前，必须为目标进程启用页堆。 请参阅以下 "备注" 部分中的详细信息。

<span id="_______-srch______"></span><span id="_______-SRCH______"></span> **-srch**   
扫描给定模式的所有堆。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span>*模式*   
指定要查找的模式。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span>*大小*   
可以是以下选项中的任何一个。 这将指定模式的大小。 "-" 是必需的。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-b</strong></p></td>
<td align="left"><p>模式大小为1个字节。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-w</strong></p></td>
<td align="left"><p>模式为一个大小的单词。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-d</strong></p></td>
<td align="left"><p>模式为一个 DWORD 大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-q</strong></p></td>
<td align="left"><p>模式为大小为1个 QWORD。</p></td>
</tr>
</tbody>
</table>

 

如果未指定上述任何一个，则假设模式的大小与计算机指针的大小相同。

<span id="_______-flt______"></span><span id="_______-FLT______"></span> **-flt**   
将显示范围限制为仅包含具有指定大小或大小范围的堆。

<span id="_______FilterOptions______"></span><span id="_______filteroptions______"></span><span id="_______FILTEROPTIONS______"></span>*FilterOptions*   
可以是以下选项中的任何一个。 *FilterOptions*区分大小写。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>s</strong> <em>大小</em></p></td>
<td align="left"><p>将显示范围限制为仅包含指定大小的堆。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong> SizeMin <em>SizeMax</em></p></td>
<td align="left"><p>将显示范围限制为仅包含指定大小范围内的堆。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-stat______"></span><span id="_______-STAT______"></span> **-stat**   
显示指定堆的使用情况统计信息。

<span id="_______-h________Handle______"></span><span id="_______-h________handle______"></span><span id="_______-H________HANDLE______"></span> **-h** *句柄*   
导致显示仅显示在*句柄*上的堆的使用情况统计信息。 如果*Handle*为0或省略，则显示所有堆的使用情况统计信息。

<span id="_______-grp________GroupBy______"></span><span id="_______-grp________groupby______"></span><span id="_______-GRP________GROUPBY______"></span> **-grp** *GroupBy*   
按*GroupBy*指定的重新排序显示。 可以在下表中找到*GroupBy*的选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">效果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>A</strong></p></td>
<td align="left"><p>根据分配大小显示使用情况统计信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>B</strong></p></td>
<td align="left"><p>根据块计数显示使用情况统计信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>S</strong></p></td>
<td align="left"><p>根据每个分配的总大小显示使用量统计信息。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______MaxDisplay______"></span><span id="_______maxdisplay______"></span><span id="_______MAXDISPLAY______"></span>*MaxDisplay*   
将输出限制为仅*MaxDisplay*的行数。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p></p>
Ext .dll Exts</td>
</tr>
</tbody>
</table>

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关堆的信息，请参阅以下资源：

通讯*Microsoft Windows 内部*的 Russinovich 和 David 所罗门群岛。

[Example 11：启用页堆验证 @ no__t-0

[Example 12：使用页堆验证查找 Bug @ no__t

有关使用堆内存处理记录器的信息，请参阅 [Example 11：启动专用跟踪会话 @ no__t-0

<a name="remarks"></a>备注
-------

此扩展命令可用于执行各种任务。

标准 **！堆**命令用于显示当前进程的堆信息。 （这应该只用于用户模式进程。 [ **！ Pool**](-pool.md) extension 命令应用于系统进程。）

**！堆-b**和 **！堆-b**命令用于在堆管理器中创建和删除条件断点。

**！堆-l**命令检测泄漏的堆块。 它使用垃圾回收器算法来检测未在进程地址空间中的任何位置引用的堆中的所有繁忙块。 对于大型应用程序，可能需要几分钟才能完成。 此命令仅在 Windows XP 和更高版本的 Windows 中可用。

**！堆-x**命令搜索包含给定地址的堆块。 如果使用了 **-v**选项，则此命令将另外在当前进程的整个虚拟内存空间中搜索指向此堆块的指针。 此命令仅在 Windows XP 和更高版本的 Windows 中可用。

**！堆-p**命令显示了各种形式的页堆信息。 使用 **！堆-p**之前，必须为目标进程启用页堆。 这是通过全局标志（gflags）实用程序来完成的。 为此，请启动实用工具，在 "**映像文件**" 文本框中填写目标应用程序的名称，选择 "**图像文件选项**" 并**启用页堆**，并单击 "**应用**"。 或者，你可以通过键入**gflags/i** *xxx* **+ hpa**（其中， *xxx*是目标应用程序的名称）从命令提示符窗口启动全局标志实用程序。

不支持在 Windows XP 以外的情况 **！堆-p-t @ no__t-1c | s @ no__t**命令。 使用随调试器包一起提供的[UMDH](umdh.md)工具来获取类似的结果。

**！ Srch**命令显示包含某个指定模式的堆条目。

**！ Flt**命令会将显示范围限制为仅指定大小的堆分配。

**！堆-stat**命令显示堆使用情况统计信息。

下面是标准 **！堆**命令的示例：

```dbgcmd
0:000> !ntsdexts.heap -a
Index   Address  Name      Debugging options enabled
  1:   00250000 
    Segment at 00250000 to 00350000 (00056000 bytes committed)
    Flags:               50000062
    ForceFlags:          40000060
    Granularity:         8 bytes
    Segment Reserve:     00100000
    Segment Commit:      00004000
    DeCommit Block Thres:00000400
    DeCommit Total Thres:00002000
    Total Free Size:     000003be
    Max. Allocation Size:7ffddfff
    Lock Variable at:    00250b54
    Next TagIndex:       0012
    Maximum TagIndex:    07ff
    Tag Entries:         00350000
    PsuedoTag Entries:   00250548
    Virtual Alloc List:  00250050
    UCR FreeList:        002504d8
    128-bit bitmap of free lists
    FreeList Usage:      00000014 00000000 00000000 00000000
              Free    Free
              List    List
#       Head      Blink      Flink
    FreeList[ 00 ] at 002500b8: 002a4378 . 002a4378
                                0x02 - HEAP_ENTRY_EXTRA_PRESENT
                                0x04 - HEAP_ENTRY_FILL_PATTERN
        Entry     Prev    Cur   0x10 - HEAP_ENTRY_LAST_ENTRY

Address   Size    Size  flags
002a4370: 00098 . 01c90 [14] - free
    FreeList[ 02 ] at 002500c8: 0025cb30 . 002527b8
002527b0: 00058 . 00010 [04] - free
0025cb28: 00088 . 00010 [04] - free
    FreeList[ 04 ] at 002500d8: 00269a08 . 0026e530
0026e528: 00038 . 00020 [04] - free
0026a4d0: 00038 . 00020 [06] - free
0026f9b8: 00038 . 00020 [04] - free
0025cda0: 00030 . 00020 [06] - free
00272660: 00038 . 00020 [04] - free
0026ab60: 00038 . 00020 [06] - free
00269f20: 00038 . 00020 [06] - free
00299818: 00038 . 00020 [04] - free
0026c028: 00038 . 00020 [06] - free
00269a00: 00038 . 00020 [46] - free
 
    Segment00 at 00250b90:
Flags:           00000000
Base:            00250000
First Entry:     00250bc8
Last Entry:      00350000
Total Pages:     00000080
Total UnCommit:  00000055
Largest UnCommit:000aa000
UnCommitted Ranges: (1)
    002a6000: 000aa000

    Heap entries for Segment00 in Heap 250000
                        0x01 - HEAP_ENTRY_BUSY            
                        0x02 - HEAP_ENTRY_EXTRA_PRESENT   
                        0x04 - HEAP_ENTRY_FILL_PATTERN    
                        0x08 - HEAP_ENTRY_VIRTUAL_ALLOC   
                        0x10 - HEAP_ENTRY_LAST_ENTRY      
                        0x20 - HEAP_ENTRY_SETTABLE_FLAG1  
                        0x40 - HEAP_ENTRY_SETTABLE_FLAG2  
Entry     Prev    Cur   0x80 - HEAP_ENTRY_SETTABLE_FLAG3  

Address   Size    Size  flags       (Bytes used)    (Tag name)
00250000: 00000 . 00b90 [01] - busy (b90)
00250b90: 00b90 . 00038 [01] - busy (38) 
00250bc8: 00038 . 00040 [07] - busy (24), tail fill (NTDLL!LDR Database)
00250c08: 00040 . 00060 [07] - busy (48), tail fill (NTDLL!LDR Database)
00250c68: 00060 . 00028 [07] - busy (10), tail fill (NTDLL!LDR Database)
00250c90: 00028 . 00060 [07] - busy (48), tail fill (NTDLL!LDR Database)
00250cf0: 00060 . 00050 [07] - busy (38), tail fill (Objects=  80)
00250d40: 00050 . 00048 [07] - busy (2e), tail fill (NTDLL!LDR Database)
00250d88: 00048 . 00c10 [07] - busy (bf4), tail fill (Objects>1024)
00251998: 00c10 . 00030 [07] - busy (12), tail fill (NTDLL!LDR Database)
...
002525c0: 00030 . 00060 [07] - busy (48), tail fill (NTDLL!LDR Database)
00252620: 00060 . 00050 [07] - busy (38), tail fill (NTDLL!LDR Database)
00252670: 00050 . 00040 [07] - busy (22), tail fill (NTDLL!CSRSS Client)
002526b0: 00040 . 00040 [07] - busy (24), tail fill (Objects=  64)
002526f0: 00040 . 00040 [07] - busy (24), tail fill (Objects=  64)
00252730: 00040 . 00028 [07] - busy (10), tail fill (Objects=  40)
00252758: 00028 . 00058 [07] - busy (3c), tail fill (Objects=  88)
002527b0: 00058 . 00010 [04] free fill
002527c0: 00010 . 00058 [07] - busy (3c), tail fill (NTDLL!LDR Database)
00252818: 00058 . 002d0 [07] - busy (2b8), tail fill (Objects= 720)
00252ae8: 002d0 . 00330 [07] - busy (314), tail fill (Objects= 816)
00252e18: 00330 . 00330 [07] - busy (314), tail fill (Objects= 816)
00253148: 00330 . 002a8 [07] - busy (28c), tail fill (NTDLL!LocalAtom)
002533f0: 002a8 . 00030 [07] - busy (18), tail fill (NTDLL!LocalAtom)
00253420: 00030 . 00030 [07] - busy (18), tail fill (NTDLL!LocalAtom)
00253450: 00030 . 00098 [07] - busy (7c), tail fill (BASEDLL!LMEM)
002534e8: 00098 . 00060 [07] - busy (44), tail fill (BASEDLL!TMP)
00253548: 00060 . 00020 [07] - busy (1), tail fill (Objects=  32)
00253568: 00020 . 00028 [07] - busy (10), tail fill (Objects=  40)
00253590: 00028 . 00030 [07] - busy (16), tail fill (Objects=  48)
...
0025ccb8: 00038 . 00060 [07] - busy (48), tail fill (NTDLL!LDR Database)
0025cd18: 00060 . 00058 [07] - busy (3c), tail fill (NTDLL!LDR Database)
0025cd70: 00058 . 00030 [07] - busy (18), tail fill (NTDLL!LDR Database)
0025cda0: 00030 . 00020 [06] free fill (NTDLL!Temporary)
0025cdc0: 00020 . 00258 [07] - busy (23c), tail fill (Objects= 600)
0025d018: 00258 . 01018 [07] - busy (1000), tail fill (Objects>1024)
0025e030: 01018 . 00060 [07] - busy (48), tail fill (NTDLL!LDR Database)
...
002a4190: 00028 . 00118 [07] - busy (100), tail fill (BASEDLL!GMEM)
002a42a8: 00118 . 00030 [07] - busy (18), tail fill (Objects=  48)
002a42d8: 00030 . 00098 [07] - busy (7c), tail fill (Objects= 152)
002a4370: 00098 . 01c90 [14] free fill
002a6000:      000aa000      - uncommitted bytes.
```

下面是 **！堆-l**命令的示例：

```dbgcmd
1:0:011> !heap -l
1:Heap 00170000
Heap 00280000
Heap 00520000
Heap 00b50000
Heap 00c60000
Heap 01420000
Heap 01550000
Heap 016d0000
Heap 019b0000
Heap 01b40000
Scanning VM ...
## Entry     User      Heap      Segment       Size  PrevSize  Flags

001b2958  001b2960  00170000  00000000        40        18  busy extra
001b9cb0  001b9cb8  00170000  00000000        80       300  busy extra
001ba208  001ba210  00170000  00000000        80        78  busy extra
001cbc90  001cbc98  00170000  00000000        e0        48  busy extra
001cbd70  001cbd78  00170000  00000000        d8        e0  busy extra
001cbe90  001cbe98  00170000  00000000        68        48  busy extra
001cbef8  001cbf00  00170000  00000000        58        68  busy extra
001cc078  001cc080  00170000  00000000        f8       128  busy extra
001cc360  001cc368  00170000  00000000        80        50  busy extra
001cc3e0  001cc3e8  00170000  00000000        58        80  busy extra
001fe550  001fe558  00170000  00000000       150       278  busy extra
001fe6e8  001fe6f0  00170000  00000000        48        48  busy extra
002057a8  002057b0  00170000  00000000        58        58  busy extra
00205800  00205808  00170000  00000000        48        58  busy extra
002058b8  002058c0  00170000  00000000        58        70  busy extra
00205910  00205918  00170000  00000000        48        58  busy extra
00205958  00205960  00170000  00000000        90        48  busy extra
00246970  00246978  00170000  00000000        60        88  busy extra
00251168  00251170  00170000  00000000        78        d0  busy extra user_flag
00527730  00527738  00520000  00000000        40        40  busy extra
00527920  00527928  00520000  00000000        40        80  busy extra
21 leaks detected.
```

此示例中的表包含发现的所有21个泄漏。

下面是 **！堆 x**命令的示例：

```dbgcmd
0:011> !heap 002057b8 -x
## Entry     User      Heap      Segment       Size  PrevSize  Flags

002057a8  002057b0  00170000  00170640        58        58  busy extra
```

下面是 **！堆-x v**命令的示例：

```dbgcmd
1:0:011> !heap 002057b8 -x -v
## 1:Entry     User      Heap      Segment       Size  PrevSize  Flags

002057a8  002057b0  00170000  00170640        58        58  busy extra

Search VM for address range 002057a8 - 002057ff : 00205990 (002057d0),
```

在此示例中，有一个指向地址0x00205990 的堆块的指针。

下面是 **！ flt s**命令的示例：

```dbgcmd
0:001>!heap -flt s 0x50
```

这会显示大小0x50 的所有分配。

下面是 **！ flt r**命令的示例：

```dbgcmd
0:001>!heap -flt r 0x50 0x80
```

这会显示大小介于0x50 和0x7F 之间的每个分配。

下面是 **！ srch**命令的示例。

```dbgcmd
0:001> !heap -srch 77176934
    _HEAP @ 00090000
   in HEAP_ENTRY: Size : Prev Flags - UserPtr UserSize - state
        00099A48: 0018 : 0005 [01] - 00099A50 (000000B8) - (busy)
          ole32!CALLFRAME_CACHE<INTERFACE_HELPER_CLSID>::`vftable'
    _HEAP @ 00090000
   in HEAP_ENTRY: Size : Prev Flags - UserPtr UserSize - state
        00099B58: 0018 : 0005 [01] - 00099B60 (000000B8) - (busy)
          ole32!CALLFRAME_CACHE<INTERFACE_HELPER_CLSID>::`vftable'
```

下图显示了堆块的排列方式。

浅页堆块--已分配：

```dbgcmd
 +-----+---------------+---+                                  
 |     |               |   |                                  
 +-----+---------------+---+                                  
    ^         ^          ^                                    
    |         |          8 suffix bytes (filled with 0xA0)    
    |         User allocation (filled with E0 if zeroing not requested) 
    Block header (starts with 0xABCDAAAA and ends with 0xDCBAAAAA) 
```

浅页堆块--已释放：

```dbgcmd
 +-----+---------------+---+                                  
 |     |               |   |                                  
 +-----+---------------+---+                                  
    ^         ^          ^                                    
    |         |          8 suffix bytes (filled with 0xA0)    
    |         User allocation (filled with F0 bytes)          
    Block header (starts with 0xABCDAAA9 and ends with 0xDCBAAA9) 
```

整页堆块--已分配：

```dbgcmd
 +-----+---------+---+-------                                 
 |     |         |   |  ... N/A page                          
 +-----+---------+---+-------                                 
    ^       ^      ^                                          
    |       |      0-7 suffix bytes (filled with 0xD0)        
    |       User allocation (if zeroing not requested, filled   
            with C0)       
    Block header (starts with 0xABCDBBBB and ends with 0xDCBABBBB) 
```

整页堆块--已释放：

```dbgcmd
 +-----+---------+---+-------                                 
 |     |         |   |  ... N/A page                          
 +-----+---------+---+-------                                 
    ^       ^      ^                                          
    |       |      0-7 suffix bytes (filled with 0xD0)        
    |       User allocation (filled with F0 bytes)            
    Block header (starts with 0xABCDBBA and ends with 0xDCBABBBA) 
```

若要查看分配的堆栈跟踪或释放堆块或完整页面堆块，请使用带有标头地址的[**DT DPH @ no__t-2BLOCK @ no__t-3INFORMATION**](dt--display-type-.md) ，后面跟有块**StackTrace**字段的[**dds**](dds--dps--dqs--display-words-and-symbols-.md) 。
