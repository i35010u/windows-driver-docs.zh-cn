---
title: poolfind
description: Poolfind 扩展在任一非分页或分页内存池查找某个特定集标记的所有实例。
ms.assetid: 01783b6b-0117-49ca-87ca-bbe3c1b0e730
keywords:
- poolfind Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- poolfind
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b774ea44405fe0208fc293369f48ff56f2a370fc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335866"
---
# <a name="poolfind"></a>!poolfind


**！ Poolfind**扩展在任一非分页或分页内存池查找某个特定集标记的所有实例。

```dbgcmd
!poolfind TagString [PoolType] 
!poolfind TagValue [PoolType] 
```

## <a name="span-idddkpoolfinddbgspanspan-idddkpoolfinddbgspanparameters"></a><span id="ddk__poolfind_dbg"></span><span id="DDK__POOLFIND_DBG"></span>参数


<span id="_______TagString______"></span><span id="_______tagstring______"></span><span id="_______TAGSTRING______"></span> *TagString*   
指定的池标记。 *TagString*是区分大小写的 ASCII 字符串。 星号 (\*) 可以用于表示任意数量的字符; 问号 （？） 可以用于表示一个字符。 除非使用一个星号，否则*TagString*必须是长度为四个字符。

<span id="_______TagValue______"></span><span id="_______tagvalue______"></span><span id="_______TAGVALUE______"></span> *TagValue*   
指定的池标记。 *TagValue*必须以"0x"开头，即使默认基数为 16。 如果此参数以与任何其他值 （包括"0x"），则它将解释为 ASCII 标记字符串。

<span id="_______PoolType______"></span><span id="_______pooltype______"></span><span id="_______POOLTYPE______"></span> *PoolType*   
指定要搜索的池的类型。 允许使用以下值：

<span id="0"></span>0  
指定非分页的内存池。 这是默认设置。

<span id="1"></span>1  
指定分页的内存池。

<span id="2"></span>2  
指定特殊的池。

<span id="4"></span>4  
指定的会话池。

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

内存池和池标记有关的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。

<a name="remarks"></a>备注
-------

此命令可能需要大量的时间来执行，具体取决于必须要搜索的池内存大小。 若要加快此执行，增加使用的 COM 端口速度[ **CTRL + A （切换波特率）** ](ctrl-a--toggle-baud-rate-.md)密钥，或使用[ **.cache （设置缓存大小）** ](-cache--set-cache-size-.md)命令来增加缓存大小 （为约为 10 MB)。

池标记是相同的标记传递给 **ExAllocate * * * Xxx*系列的例程。

下面是一个示例。 搜索整个非分页缓冲的池，然后搜索页面缓冲的池，但命令终止之前完成 （后一小时的操作）：

```dbgcmd
kd> !poolfind SeSd 0

Scanning large pool allocation table for Tag: SeSd (827d1000 : 827e9000)

Searching NonPaged pool (823b1000 : 82800000) for Tag: SeSd

826fa130 size:   c0 previous size:   40  (Allocated) SeSd
82712000 size:   c0 previous size:    0  (Allocated) SeSd
82715940 size:   a0 previous size:   60  (Allocated) SeSd
8271da30 size:   c0 previous size:   10  (Allocated) SeSd
82721c00 size:   10 previous size:   30  (Free)      SeSd
8272b3f0 size:   60 previous size:   30  (Allocated) SeSd
8272d770 size:   60 previous size:   40  (Allocated) SeSd
8272d7d0 size:   a0 previous size:   60  (Allocated) SeSd
8272d960 size:   a0 previous size:   70  (Allocated) SeSd
82736f30 size:   a0 previous size:   10  (Allocated) SeSd
82763840 size:   a0 previous size:   10  (Allocated) SeSd
8278b730 size:  100 previous size:  290  (Allocated) SeSd
8278b830 size:   10 previous size:  100  (Free)      SeSd
82790130 size:   a0 previous size:   20  (Allocated) SeSd
82799180 size:   a0 previous size:   10  (Allocated) SeSd
827c00e0 size:   a0 previous size:   30  (Allocated) SeSd
827c8320 size:   a0 previous size:   60  (Allocated) SeSd
827ca180 size:   a0 previous size:   50  (Allocated) SeSd
827ec140 size:   a0 previous size:   10  (Allocated) SeSd

Searching NonPaged pool (fe7c3000 : ffbe0000) for Tag: SeSd

kd> !poolfind SeSd 1

Scanning large pool allocation table for Tag: SeSd (827d1000 : 827e9000)

Searching Paged pool (e1000000 : e4400000) for Tag: SeSd

e10000b0 size:   d0 previous size:   20  (Allocated) SeSd
e1000260 size:   d0 previous size:   60  (Allocated) SeSd
......
e1221dc0 size:   a0 previous size:   60  (Allocated) SeSd
e1224250 size:   a0 previous size:   30  (Allocated) SeSd

...terminating - searched pool to e1224000
kd> 
```

 

 





