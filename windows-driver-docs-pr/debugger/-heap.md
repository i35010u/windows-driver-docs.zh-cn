---
title: 堆
description: 堆扩展显示堆使用情况信息、 控制堆管理器中的断点，检测到泄漏的堆阻止搜索堆的块，或显示页堆信息。
ms.assetid: 70947b56-1a8c-4e78-85d0-d5df87f3150c
keywords:
- 堆使用情况
- GFlags、 启用页堆
- Windows 调试堆
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- heap
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5551b7ee85e5b7cd7f01635e76a7f87bad472c87
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575409"
---
# <a name="heap"></a>!heap


**！ 堆**扩展显示堆使用情况信息、 控制堆管理器中的断点，检测到泄漏的堆阻止搜索堆的块，或显示页堆信息。

此扩展插件支持段堆和 NT 堆。 使用 ！ 堆不使用任何参数，以列出所有堆和它们的类型。

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

## <a name="span-idsegmentandntheapparametersspanspan-idsegmentandntheapparametersspanspan-idsegmentandntheapparametersspansegment-and-nt-heap-parameters"></a><span id="Segment_and_NT_Heap_Parameters"></span><span id="segment_and_nt_heap_parameters"></span><span id="SEGMENT_AND_NT_HEAP_PARAMETERS"></span>段和 NT 堆参数


这些参数适用于段和 NT 堆。

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
指定正在请求的摘要信息。 如果*SummaryOptions*并*StatHeapAddress*省略，则为当前进程与堆关联的所有显示的摘要信息。

<span id="_______SummaryOptions______"></span><span id="_______summaryoptions______"></span><span id="_______SUMMARYOPTIONS______"></span> *SummaryOptions*   
可以是下列选项中的任意组合。 *SummaryOptions*不区分大小写。 类型 ！ 堆-s-？ 有关其他信息。

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
<td align="left"><p><strong>-b</strong>  <em>BucketSize</em></p></td>
<td align="left"><p>指定存储桶大小。 默认值为 1024 位。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-d</strong>  <em>DumpBlockSize</em></p></td>
<td align="left"><p>指定存储桶大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-a</strong></p></td>
<td align="left"><p>转储堆的所有块。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-c</strong></p></td>
<td align="left"><p>指定应显示每个块的内容。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-triage__Handle___Address___"></span><span id="_______-triage__handle___address___"></span><span id="_______-TRIAGE__HANDLE___ADDRESS___"></span> **-会审\[** <em>处理</em> **|** <em>地址</em>**\]**   
使调试器能够自动搜索中的进程的堆中的失败。 如果堆处理指定为参数，检查该堆;否则为所有堆中都搜索包含给定的地址，并且如果找到一个对象，对其进行检查。 使用 **-会审**是验证低分片堆 (LFH) 损坏的唯一方法。

<span id="_______-x_-v_"></span><span id="_______-X_-V_"></span> **-x** **** \[**-v**\]   
使调试器要搜索包含指定的地址的堆块。 如果添加-v，则此命令会搜索当前过程对于指向此堆块的整个虚拟内存空间。

<span id="_______-l______"></span><span id="_______-L______"></span> **-l**   
调试器以检测泄漏的原因堆块。

<span id="_______-i________Address______-h_HeapAddress______"></span><span id="_______-i________address______-h_heapaddress______"></span><span id="_______-I________ADDRESS______-H_HEAPADDRESS______"></span> **-i** **** *Address* **-h** *HeapAddress*   
显示有关指定的信息*堆*。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要搜索的地址。

<span id="_______-_______"></span> **-?**   
在调试器命令窗口中显示此扩展的一些简要帮助文本。 使用 **！ 堆的？** 有关泛型的帮助，和 **！ 堆-p-？** 有关页面堆帮助。

## <a name="span-idddkheapdbgspanspan-idddkheapdbgspannt-heap-parameters"></a><span id="ddk__heap_dbg"></span><span id="DDK__HEAP_DBG"></span>NT 堆参数


这些参数只使用 NT 堆。

<span id="_______HeapOptions______"></span><span id="_______heapoptions______"></span><span id="_______HEAPOPTIONS______"></span> *HeapOptions*   
可以是下列选项中的任意组合。 *HeapOptions*值是区分大小写。

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
<td align="left"><p>使调试器来验证指定的堆。</p>
<div class="alert">
<strong>请注意</strong>  此选项不会检测低碎片堆 (LFH) 损坏。 使用<strong>-会审</strong>相反。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-a</strong></p></td>
<td align="left"><p>将导致显示以包括指定堆的所有信息。 大小，在这种情况下，舍入为堆粒度。 (运行<strong>！ 堆</strong>与<strong>-a</strong>选项相当于使用三个选项运行它<strong>-h f-m</strong>，这可能需要长时间。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-h</strong></p></td>
<td align="left"><p>将导致显示以包括指定堆的所有非 LFH 条目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-hl</strong></p></td>
<td align="left"><p>将导致显示效果以包括指定堆，包括 LFH 条目的所有条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-f</strong></p></td>
<td align="left"><p>将导致显示以包括指定堆的所有可用的列表项。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-m</strong></p></td>
<td align="left"><p>将导致显示效果以包括指定堆的所有段条目。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-t</strong></p></td>
<td align="left"><p>将导致显示以包括指定堆的标记信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-T</strong></p></td>
<td align="left"><p>将导致显示以包括指定堆的伪标记项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-g</strong></p></td>
<td align="left"><p>将导致显示以包括全局标记信息。 全局标记是与每个未标记分配相关联。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-s</strong></p></td>
<td align="left"><p>将导致显示以包括指定堆的摘要信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-k</strong></p></td>
<td align="left"><p>（仅基于 x86 的目标）将导致显示以包括与每个条目相关联的堆栈反向跟踪。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______ValidationOptions______"></span><span id="_______validationoptions______"></span><span id="_______VALIDATIONOPTIONS______"></span> *ValidationOptions*   
可以是任何单个的以下选项之一。 *ValidationOptions*区分大小写。

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
<td align="left"><p>禁用验证的电话技术支持为指定的堆。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-E</strong></p></td>
<td align="left"><p>允许验证-上的调用为指定的堆。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-d</strong></p></td>
<td align="left"><p>禁用堆检查指定的堆。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-e</strong></p></td>
<td align="left"><p>可以检查指定的堆的堆。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-i________Heap_Address______or_HeapAddress______"></span><span id="_______-i________heap_address______or_heapaddress______"></span><span id="_______-I________HEAP_ADDRESS______OR_HEAPADDRESS______"></span> **-i** **** *Heap* **** *Address* **or** *HeapAddress*   
显示有关指定的信息*堆*。

<span id="_______BreakAddress______"></span><span id="_______breakaddress______"></span><span id="_______BREAKADDRESS______"></span> *BreakAddress*   
指定要设置或删除断点的位置的块的地址。

<span id="_______-b______"></span><span id="_______-B______"></span> **-b**   
使调试器在堆管理器中创建条件断点。 **-B**选项可以后跟**alloc**， **realloc**，或**免费**; 这会指定是否将通过激活断点分配、 重新分配，或释放内存。 如果*BreakAddress*是用来指定块的地址，就可以省略的断点类型。 如果*堆*是用来指定堆地址或堆索引，该类型必须包含在内，并将*标记*参数。

<span id="_______Tag______"></span><span id="_______tag______"></span><span id="_______TAG______"></span> *标记*   
指定在堆中的标记名。

<span id="_______-B______"></span><span id="_______-b______"></span> **-B**   
使调试器从堆管理器中删除条件断点。 断点类型 (**alloc**， **realloc**，或**免费**)，则必须指定并且必须与用于相同 **-b**选项。

<span id="_______StatHeapAddress______"></span><span id="_______statheapaddress______"></span><span id="_______STATHEAPADDRESS______"></span> *StatHeapAddress*   
指定在堆的地址。 如果这是 0 或被省略，将显示所有当前进程与堆关联。

<span id="_______-p______"></span><span id="_______-P______"></span> **-p**   
指定为其请求页堆信息。 如果这使用不带任何*PageHeapOptions*，将显示堆的所有页面。

<span id="_______PageHeapOptions______"></span><span id="_______pageheapoptions______"></span><span id="_______PAGEHEAPOPTIONS______"></span> *PageHeapOptions*   
可以是任何单个的以下选项之一。 *PageHeapOptions*区分大小写。 如果未不指定任何选项，则将显示所有可能的页堆句柄。

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
<td align="left"><p><strong>-h</strong>  <em>Handle</em></p></td>
<td align="left"><p>使调试器显示详细的信息页堆句柄<em>处理</em>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-a</strong>  <em>Address</em></p></td>
<td align="left"><p>导致调试器来查找其块包含在页堆<em>地址</em>。 如何与此地址关联到整页堆块的完整详细信息将包括在内，例如此地址是否为页堆，它在块内的偏移量的一部分，以及是否在块被分配或已释放。 可用时，将包含堆栈跟踪。 使用此选项时，会显示大小的倍数堆分配粒度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-t</strong>[<strong>c</strong>|<strong>s</strong>]  [<em>Traces</em>]</p></td>
<td align="left"><p>使调试器要显示的大量堆用户收集的跟踪。 <em>跟踪</em>指定要显示; 的跟踪号默认值为 4。 如果有超过指定的详细跟踪，会显示最早的跟踪。 如果<strong>-t</strong>或<strong>-tc</strong>是使用，跟踪将按计数使用情况。 如果<strong>-ts</strong>是使用，按大小排序的跟踪。 ( <strong>-Tc</strong>并<strong>-ts</strong>选项; 仅支持在 Windows XP <strong>-t</strong>仅在 Windows XP 和 Windows 的早期版本中支持选项。)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-fi</strong>  [<em>Traces</em>]</p></td>
<td align="left"><p>使调试器用于显示最新的故障注入跟踪。 <em>跟踪</em>指定数量来显示; 默认值为 4。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-all</strong></p></td>
<td align="left"><p>使调试器，堆显示有关所有页面的详细的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-?</strong></p></td>
<td align="left"><p>使调试器显示页堆帮助，包括堆块的关系图。 （这些关系图，也会看到以下备注部分中。）</p></td>
</tr>
</tbody>
</table>

 

你可以使用任何之前 **！ 堆-p**扩展命令时，必须为目标进程启用页堆。 请参阅以下备注部分中的详细信息。

<span id="_______-srch______"></span><span id="_______-SRCH______"></span> **-srch**   
扫描所有堆给定模式。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *Pattern*   
指定要查找的模式。

<span id="_______Size______"></span><span id="_______size______"></span><span id="_______SIZE______"></span> *大小*   
可以是任何单个的以下选项之一。 这用于指定模式的大小。 -是必需的。

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
<td align="left"><p>模式是一个字节的大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-w</strong></p></td>
<td align="left"><p>模式是一个单词的大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-d</strong></p></td>
<td align="left"><p>模式是一个 DWORD 的大小。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-q</strong></p></td>
<td align="left"><p>模式是一个 QWORD 的大小。</p></td>
</tr>
</tbody>
</table>

 

如果指定了上述任何订阅，然后被假定该模式可作为机指针大小相同。

<span id="_______-flt______"></span><span id="_______-FLT______"></span> **-flt**   
限制显示以包括仅与指定的大小或大小范围的堆。

<span id="_______FilterOptions______"></span><span id="_______filteroptions______"></span><span id="_______FILTEROPTIONS______"></span> *FilterOptions*   
可以是任何单个的以下选项之一。 *FilterOptions*区分大小写。

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
<td align="left"><p><strong>s</strong>  <em>Size</em></p></td>
<td align="left"><p>限制显示以包括仅指定大小的堆。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r</strong>  <em>SizeMin</em>  <em>SizeMax</em></p></td>
<td align="left"><p>限制显示以包括仅在指定的大小范围内的堆。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______-stat______"></span><span id="_______-STAT______"></span> **-stat**   
显示指定堆的使用情况统计信息。

<span id="_______-h________Handle______"></span><span id="_______-h________handle______"></span><span id="_______-H________HANDLE______"></span> **-h** *Handle*   
导致仅在堆的使用情况统计*处理*显示。 如果*处理*为 0 或省略，则对于所有堆使用情况统计信息会显示。

<span id="_______-grp________GroupBy______"></span><span id="_______-grp________groupby______"></span><span id="_______-GRP________GROUPBY______"></span> **-grp** **** *GroupBy*   
对显示为指定的重新排序*GroupBy*。 选项*GroupBy*可发现下表中。

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
<td align="left"><p>显示分配的大小根据使用情况统计信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>B</strong></p></td>
<td align="left"><p>显示根据块计数使用情况统计信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>S</strong></p></td>
<td align="left"><p>显示每个分配的总大小根据使用情况统计信息。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______MaxDisplay______"></span><span id="_______maxdisplay______"></span><span id="_______MAXDISPLAY______"></span> *MaxDisplay*   
将输出限制为仅*MaxDisplay*的行数。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p></p>
Ext.dll Exts.dll</td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关堆的信息，请参阅 Microsoft Windows SDK 文档，Windows Driver Kit (WDK) 文档，并*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

此扩展命令可以用于执行各种任务。

标准 **！ 堆**命令用于显示当前进程堆信息。 （这应该是仅用于用户模式进程。 [ **！ 池**](-pool.md)扩展命令应该用于系统进程。)

**！ 堆-b**并 **！ 堆-B**命令用于创建和删除堆管理器中的条件断点。

**！ 堆-l**命令检测泄漏的堆块。 它使用垃圾回收器算法来检测所有忙块与未在进程地址空间中任何位置引用的堆。 对于大型应用程序，可能需要几分钟才能完成。 此命令才在 Windows XP 和更高版本的 Windows 中可用。

**！ 堆-x**命令搜索包含给定的地址的堆块。 如果 **-v**选项，则此命令将此外搜索当前过程对于指向此堆块的整个虚拟内存空间。 此命令才在 Windows XP 和更高版本的 Windows 中可用。

**！ 堆-p**命令显示各种形式的页面堆信息。 使用之前 **！ 堆-p**，必须启用目标进程在页堆。 这是通过全局标志 (gflags.exe) 实用程序。 若要执行此操作，启动该实用程序，填写名称中的目标应用程序**图像文件名**文本框中，选择**图像文件选项**并**启用页堆**，然后单击**应用**。 或者，通过键入，在命令提示符窗口中启动的全局标志实用工具**gflags /i** *xxx.exe* **+ hpa**，其中*xxx.exe*是目标应用程序的名称。

**！ 堆-p-t\[c | s\]** 超出了 Windows XP 不支持命令。 使用[UMDH](umdh.md)调试器包来获取类似的结果中随附的工具。

**！ 堆-srch**命令显示包含某些指定的模式的堆条目。

**！ 堆-flt**命令将显示以仅堆分配指定大小的限制。

**！ 堆-stat**命令显示堆使用情况统计信息。

下面是标准的示例 **！ 堆**命令：

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

下面是举例 **！ 堆-l**命令：

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

此示例中的表包含找到的所有 21 泄漏。

下面是举例 **！ 堆-x**命令：

```dbgcmd
0:011> !heap 002057b8 -x
## Entry     User      Heap      Segment       Size  PrevSize  Flags

002057a8  002057b0  00170000  00170640        58        58  busy extra
```

下面是举例 **！ 堆-x-v**命令：

```dbgcmd
1:0:011> !heap 002057b8 -x -v
## 1:Entry     User      Heap      Segment       Size  PrevSize  Flags

002057a8  002057b0  00170000  00170640        58        58  busy extra

Search VM for address range 002057a8 - 002057ff : 00205990 (002057d0),
```

在此示例中，没有在地址 0x00205990 此堆块的指针。

下面是举例 **！ 堆-flt s**命令：

```dbgcmd
0:001>!heap -flt s 0x50
```

这将显示所有的分配大小 0x50。

下面是举例 **！ 堆-flt r**命令：

```dbgcmd
0:001>!heap -flt r 0x50 0x80
```

这将显示每个分配，其大小是 0x50 和 0x7F 之间。

下面是举例 **！ 堆-srch**命令。

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

下图显示堆块的排列方式。

浅页堆块-分配：

```dbgcmd
 +-----+---------------+---+                                  
 |     |               |   |                                  
 +-----+---------------+---+                                  
    ^         ^          ^                                    
    |         |          8 suffix bytes (filled with 0xA0)    
    |         User allocation (filled with E0 if zeroing not requested) 
    Block header (starts with 0xABCDAAAA and ends with 0xDCBAAAAA) 
```

浅页堆块-释放：

```dbgcmd
 +-----+---------------+---+                                  
 |     |               |   |                                  
 +-----+---------------+---+                                  
    ^         ^          ^                                    
    |         |          8 suffix bytes (filled with 0xA0)    
    |         User allocation (filled with F0 bytes)          
    Block header (starts with 0xABCDAAA9 and ends with 0xDCBAAA9) 
```

整页堆块-分配：

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

整页堆块-释放：

```dbgcmd
 +-----+---------+---+-------                                 
 |     |         |   |  ... N/A page                          
 +-----+---------+---+-------                                 
    ^       ^      ^                                          
    |       |      0-7 suffix bytes (filled with 0xD0)        
    |       User allocation (filled with F0 bytes)            
    Block header (starts with 0xABCDBBA and ends with 0xDCBABBBA) 
```

若要查看堆栈跟踪的分配或释放堆块或页填满堆块，请使用[ **dt DPH\_块\_信息**](dt--display-type-.md)标头地址后, 跟[**dds** ](dds--dps--dqs--display-words-and-symbols-.md)使用的块**StackTrace**字段。

 

 





