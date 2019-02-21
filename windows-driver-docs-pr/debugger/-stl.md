---
title: stl
description: Stl 扩展显示的一些已知的标准模板库 (STL) 模板。
ms.assetid: a1f1f923-64bd-44c9-941f-9a648888c7e0
keywords:
- stl Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- stl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a00d9bc1f14bab55c2bed449ed6129a1d136fc4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521396"
---
# <a name="stl"></a>!stl


**！ Stl**扩展显示的一些已知的标准模板库 (STL) 模板。

```dbgcmd
!stl [Options] Template 
!stl -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
可以包含任何以下可能性：

<span id="-v"></span><span id="-V"></span>**-v**  
原因的详细输出显示。

<span id="-V"></span><span id="-v"></span>**-V**  
会使更多详细的输出显示，例如有关进度的扩展，包括当某些函数调用，并且将其返回信息。

<span id="_______Template______"></span><span id="_______template______"></span><span id="_______TEMPLATE______"></span> *模板*   
指定要显示的模板的名称。

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
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果启用了调试器的详细模式的详细的选项才会生效。

此扩展当前支持以下类型的 STL 模板： string、 wstring、 向量&lt;*字符串*&gt;，向量&lt;*wstring*&gt;，列表&lt;*字符串*&gt;，列表&lt;*wstring*&gt;，和任何上述类型的指针。

 

 





