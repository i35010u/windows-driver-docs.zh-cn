---
title: stl
description: Stl 扩展显示某些已知的标准模板库 (STL) 模板。
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
ms.openlocfilehash: d6e4c592aa45eb93701d863c0292acd0c2a0a528
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819407"
---
# <a name="stl"></a>!stl


**！！** Extension 显示某些已知的标准模板库 (stl) 模板。

```dbgcmd
!stl [Options] Template 
!stl -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
可能包含以下任意一种可能性：

<span id="-v"></span><span id="-V"></span>**-v**  
导致显示详细输出。

<span id="-V"></span><span id="-v"></span>**-V**  
导致显示更详细的输出，如有关扩展进度的信息，包括调用和返回某些函数的时间。

<span id="_______Template______"></span><span id="_______template______"></span><span id="_______TEMPLATE______"></span>*模板*   
指定要显示的模板的名称。

<span id="_______-_______"></span> **-?**   
在调试器命令窗口中显示此扩展的一些简短帮助文本。

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
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

只有启用了调试器的详细模式，详细选项才会生效。

此扩展目前支持以下类型的 STL 模板： string、wstring、vector &lt; *string* &gt; 、vector &lt; *wstring* &gt; 、list &lt; *string* &gt; 、list &lt; *wstring* &gt; 和指向上述任何类型的指针。

 

 





