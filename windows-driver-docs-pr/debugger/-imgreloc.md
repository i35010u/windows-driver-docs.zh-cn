---
title: imgreloc
description: Imgreloc 扩展显示每个已加载模块的地址，并在重定位之前指示其以前的地址。
keywords:
- imgreloc Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- imgreloc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f22202a3c274354c34c31db36c377b08bea6f9ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788971"
---
# <a name="imgreloc"></a>!imgreloc


**！ Imgreloc** extension 显示每个已加载模块的地址，并在重定位之前指示其以前的地址。

```dbgcmd
!imgreloc Address 
```

## <a name="span-idddk__imgreloc_dbgspanspan-idddk__imgreloc_dbgspanparameters"></a><span id="ddk__imgreloc_dbg"></span><span id="DDK__IMGRELOC_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定映像的基址。

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

 

<a name="remarks"></a>备注
-------

以下是示例：

```dbgcmd
0:000> !imgreloc 00400000
00400000 Prymes - at preferred address
010e0000 appvcore - RELOCATED from 00400000
5b2f0000 verifier - at preferred address
5d160000 ShimEng - at preferred address
```

 

 





