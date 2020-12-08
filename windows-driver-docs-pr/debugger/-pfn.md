---
title: pfn
description: Pfn 扩展显示特定页面框架或整个页面框架数据库的相关信息。
keywords:
- 页面框架
- pfn Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pfn
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1558f0eab360c5eee168b5af2be1152053f24476
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824739"
---
# <a name="pfn"></a>!pfn


**！ Pfn** extension 显示特定页面框架或整个页面框架数据库的相关信息。

```dbgcmd
!pfn PageFrame
```

## <a name="span-idddk__pfn_dbgspanspan-idddk__pfn_dbgspanparameters"></a><span id="ddk__pfn_dbg"></span><span id="DDK__PFN_DBG"></span>参数


<span id="_______PageFrame______"></span><span id="_______pageframe______"></span><span id="_______PAGEFRAME______"></span>*PageFrame*   
指定要显示的页面框架的十六进制数。

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

有关页表、页面目录和页面框架的信息，请参阅 *Microsoft Windows 内部机制*，其标记为 Russinovich 和 David 所罗门群岛。 

<a name="remarks"></a>备注
-------

可以通过使用 [**！ pte**](-pte.md) 扩展名获取虚拟地址的页面帧号。

下面是此扩展的输出示例：

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

 

 





