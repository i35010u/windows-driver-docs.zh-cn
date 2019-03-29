---
title: imgreloc
description: Imgreloc 扩展显示的每个已加载模块的地址，并指示其以前的地址，它们已重新定位前。
ms.assetid: 79b729bd-7e4f-4167-b049-8a5c23cb8787
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
ms.openlocfilehash: e3ab5678381a6cca0945f76a46dc13bc1c184445
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577086"
---
# <a name="imgreloc"></a>!imgreloc


**！ Imgreloc**扩展显示的每个已加载模块的地址，并指示其以前的地址，它们已重新定位前。

```dbgcmd
!imgreloc Address 
```

## <a name="span-idddkimgrelocdbgspanspan-idddkimgrelocdbgspanparameters"></a><span id="ddk__imgreloc_dbg"></span><span id="DDK__IMGRELOC_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定映像的基址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

下面是一个示例：

```dbgcmd
0:000> !imgreloc 00400000
00400000 Prymes - at preferred address
010e0000 appvcore - RELOCATED from 00400000
5b2f0000 verifier - at preferred address
5d160000 ShimEng - at preferred address
```

 

 





