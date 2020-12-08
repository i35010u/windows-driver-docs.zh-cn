---
title: poolfind
description: Poolfind 扩展在非分页或分页的内存池中查找特定池标记的所有实例。
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
ms.openlocfilehash: 921098296bc564bb82760479b3fd86efb1f530e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791711"
---
# <a name="poolfind"></a>!poolfind


**！ Poolfind** 扩展在非分页或分页的内存池中查找特定池标记的所有实例。

```dbgcmd
!poolfind TagString [PoolType] 
!poolfind TagValue [PoolType] 
```

## <a name="span-idddk__poolfind_dbgspanspan-idddk__poolfind_dbgspanparameters"></a><span id="ddk__poolfind_dbg"></span><span id="DDK__POOLFIND_DBG"></span>参数


<span id="_______TagString______"></span><span id="_______tagstring______"></span><span id="_______TAGSTRING______"></span>*TagString*   
指定池标记。 *TagString* 是一个区分大小写的 ASCII 字符串。 星号 (\*) 可用于表示任意数量的字符; 问号 (？ ) 可以用来精确表示一个字符。 除非使用星号，否则 *TagString* 的长度必须正好为四个字符。

<span id="_______TagValue______"></span><span id="_______tagvalue______"></span><span id="_______TAGVALUE______"></span>*TagValue*   
指定池标记。 即使默认基数为16， *TagValue* 也必须以 "0x" 开头。 如果此参数以任何其他值开头 (包括 "0X" ) 它将被解释为 ASCII 标记字符串。

<span id="_______PoolType______"></span><span id="_______pooltype______"></span><span id="_______POOLTYPE______"></span>*PoolType*   
指定要搜索的池的类型。 允许使用以下值：

<span id="0"></span>0  
指定非分页内存池。 这是默认值。

<span id="1"></span>1  
指定分页内存池。

<span id="2"></span>2  
指定特殊池。

<span id="4"></span>4  
指定会话池。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关内存池和池标记的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部*，并将 Russinovich 和 David 所罗门群岛标记为。

<a name="remarks"></a>备注
-------

执行此命令可能需要很长时间，具体取决于必须搜索的池内存大小。 若要加快此执行速度，请使用 [**CTRL + A (切换波特率)**](ctrl-a--toggle-baud-rate-.md) 键，或使用 [**Cache (设置缓存大小)**](-cache--set-cache-size-.md) 命令将缓存大小增加 (约 10 MB) 。

池标记是传递到 **ExAllocate**_Xxx_ 系列例程的同一标记。

示例如下。 搜索整个非分页池，然后搜索页面缓冲池，但在完成后 () 执行一小时后终止该命令：

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

 

 





