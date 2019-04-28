---
title: pfn
description: Pfn 扩展显示有关特定页边框或整个页面框架数据库的信息。
ms.assetid: cbdb1f04-30bc-4e12-b073-9882e4457e1a
keywords:
- 页面框架
- Windows 调试 pfn
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pfn
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6d1e8d1519e4c758492e47c8043461d75e9b0034
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335770"
---
# <a name="pfn"></a>!pfn


**！ Pfn**扩展显示有关特定页边框或整个页面框架数据库的信息。

```dbgcmd
!pfn PageFrame
```

## <a name="span-idddkpfndbgspanspan-idddkpfndbgspanparameters"></a><span id="ddk__pfn_dbg"></span><span id="DDK__PFN_DBG"></span>参数


<span id="_______PageFrame______"></span><span id="_______pageframe______"></span><span id="_______PAGEFRAME______"></span> *PageFrame*   
指定要显示的页框架的十六进制数。

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

页表、 页目录和页框架有关的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 

<a name="remarks"></a>备注
-------

可以通过使用获取的虚拟地址帧页码[ **！ pte** ](-pte.md)扩展。

下面是输出的来自此扩展插件示例：

```dbgcmd
kd> !pte 801544f4
801544F4  - PDE at C0300800        PTE at C0200550
          contains 0003B163      contains 00154121
        pfn 3b G-DA--KWV    pfn 154 G--A--KRV

kd> !pfn 3b
    PFN 0000003B at address 82350588
    flink       00000000  blink / share count 00000221  pteaddress C0300800
    reference count 0001                                 color 0
    restore pte 00000000  containing page        000039  Active   
 

kd> !pfn 154
    PFN 00000154 at address 82351FE0
    flink       00000000  blink / share count 00000001  pteaddress C0200550
    reference count 0001                                 color 0
    restore pte 00000060  containing page        00003B  Active     M     
    Modified          
```

 

 





