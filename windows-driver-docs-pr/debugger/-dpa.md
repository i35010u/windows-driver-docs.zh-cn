---
title: dpa
description: Dpa 扩展显示池分配信息。
ms.assetid: 1eb31741-bc50-4188-823d-b6324d2dfdf1
keywords:
- 池分配
- dpa Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dpa
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fe33605cd5d0e161f5c6cac46a8c3c982c5e6121
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576973"
---
# <a name="dpa"></a>!dpa


**！ Dpa**扩展显示池分配信息。

```dbgcmd
!dpa Options 
!dpa -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
必须有且仅以下选项之一：

<span id="-c"></span><span id="-C"></span>**-c**  
显示当前的池分配统计信息。

<span id="-v"></span><span id="-V"></span>**-v**  
显示所有当前的池分配。

<span id="-vs"></span><span id="-VS"></span>**-vs**  
将导致显示以包括堆栈跟踪。

<span id="-f"></span><span id="-F"></span>**-f**  
显示失败的池分配。

<span id="-r"></span><span id="-R"></span>**-r**  
显示可用池分配。

<span id="-p_Ptr"></span><span id="-p_ptr"></span><span id="-P_PTR"></span>**-p** **** *Ptr*  
显示包含指针的所有池分配*Ptr*。

<span id="_______-_______"></span> **-?**   
在调试器命令窗口中显示此扩展的一些简要帮助文本。

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

 

<a name="remarks"></a>备注
-------

若要运行此扩展的顺序，必须在 Win32k.sys 中启用池检测。

 

 





