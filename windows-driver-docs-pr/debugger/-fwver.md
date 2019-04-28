---
title: fwver
description: Fwver 扩展显示 Itanium 固件版本。
ms.assetid: 0b1a2fb2-9df6-45b4-bd5b-cbcdde38ddad
keywords:
- fwver Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- fwver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b70059e40e3e30233eb1900849181607d0a5cb10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336594"
---
# <a name="fwver"></a>!fwver


**！ Fwver**扩展显示 Itanium 固件版本。

```dbgcmd
!fwver 
```

**重要**  此命令已被 Windows 调试器版本 10.0.14257 中不推荐使用和更高版本，并不再可用。

 

## <span id="ddk__fwver_dbg"></span><span id="DDK__FWVER_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

此扩展命令仅用于 Itanium 目标计算机。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅 Intel 体系结构手动。

<a name="remarks"></a>备注
-------

下面是输出的来自此扩展插件示例：

```dbgcmd
kd> !fwver

Firmware Version

   Sal Revision:        0
   SAL_A_VERSION:       0
   SAL_B_VERSION:       0
   PAL_A_VERSION:       6623
   PAL_B_VERSION:       6625
   smbiosString:        W460GXBS2.86E.0117A.P08.200107261041
```

 

 





