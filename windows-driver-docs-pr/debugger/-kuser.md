---
title: kuser
description: Kuser 扩展将显示共享的用户模式页 (KUSER_SHARED_DATA)。
ms.assetid: 352a2f96-ff66-41be-94ee-045edbb1f81f
keywords:
- kuser Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- kuser
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: df0ce99c1d41011a468b0edf042aec272cf3ff63
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336205"
---
# <a name="kuser"></a>!kuser


**！ Kuser**扩展插件都会显示共享的用户模式页 (KUSER\_共享\_数据)。

```dbgcmd
!kuser 
```

## <span id="ddk__kuser_dbg"></span><span id="DDK__KUSER_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Kdextx86.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KUSER\_共享\_数据页面提供了资源和当前登录的用户有关的其他信息。

下面是一个示例。 请注意，在此示例中，计时周期计数显示在这两个其原始窗体和窗体中更加友好的用户，这是在括号中。 用户友好的显示是仅适用于 Windows XP 及更高版本。

```dbgcmd
kd> !kuser
_KUSER_SHARED_DATA at 7ffe0000
TickCount:    fa00000 * 00482006 (0:20:30:56.093)
TimeZone Id: 2
ImageNumber Range: [14c .. 14c]
Crypto Exponent: 0
SystemRoot: 'F:\WINDOWS'
```

 

 





