---
title: pocaps
description: Pocaps 扩展显示目标计算机的电源的功能。
ms.assetid: 011d923a-a5c4-4d3b-ba06-fe5dc884adaa
keywords:
- pocaps Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pocaps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ce187373b0432aafe41db47c05efd427d8f8f70f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525276"
---
# <a name="pocaps"></a>!pocaps


**！ Pocaps**扩展显示的目标计算机的电源功能。

```dbgcmd
!pocaps
```

## <span id="ddk__pocaps_dbg"></span><span id="DDK__POCAPS_DBG"></span>


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

若要查看系统的电源策略，请使用[ **！ popolicy** ](-popolicy.md)扩展命令。 有关电源功能和电源策略的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

下面是输出的此命令的示例：

```dbgcmd
kd> !pocaps
PopCapabilities @ 0x8016b100
  Misc Supported Features:  S4 FullWake
  Processor Features:      
  Disk Features:            SpinDown
  Battery Features:        
  Wake Caps
    Ac OnLine Wake:         Sx
    Soft Lid Wake:          Sx
    RTC Wake:               Sx
    Min Device Wake:        Sx
    Default Wake:           Sx
```

 

 





