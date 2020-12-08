---
title: fwver
description: Fwver 扩展显示安腾固件版本。
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
ms.openlocfilehash: 610f0a4b4eab9025c28fea1f7cf8b35f73aefca5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824795"
---
# <a name="fwver"></a>!fwver


**！ Fwver** extension 显示了安腾固件版本。

```dbgcmd
!fwver 
```

**重要提示**  此命令在 Windows 调试器版本10.0.14257 和更高版本中已弃用，不再可用。

 

## <span id="ddk__fwver_dbg"></span><span id="DDK__FWVER_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

此扩展命令只能与 Itanium 目标计算机一起使用。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 Intel 体系结构手册。

<a name="remarks"></a>备注
-------

下面是此扩展的输出示例：

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

 

 





