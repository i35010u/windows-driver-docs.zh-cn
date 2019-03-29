---
title: cppexr
description: Cppexr 扩展显示 c + + 异常记录的内容。
ms.assetid: 568c98e9-31d9-4c49-9b7a-bc8eccfed24a
keywords:
- 异常记录
- cppexr Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- cppexr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 327c2e2ab4bfde70b0363f6d66e48fdf1d1e9820
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569346"
---
# <a name="cppexr"></a>!cppexr


**！ Cppexr**扩展显示的 c + + 异常记录内容。

```dbgsyntax
    !cppexr Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要显示的 c + + 异常记录的地址。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关异常的详细信息，请参阅[控制异常和事件](controlling-exceptions-and-events.md)，Windows Driver Kit (WDK) 文档、 Windows SDK 文档中，并*Microsoft Windows Internals*标记Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）使用[ **.exr** ](-exr--display-exception-record-.md)命令以显示其他异常记录。

<a name="remarks"></a>备注
-------

**！ Cppexr**扩展显示目标遇到，包括异常代码、 异常和异常标志的地址的 c + + 异常与相关的信息。 此异常必须是一个在 Msvcrt.dll 中定义的标准 c + + 异常。

通常可以获得*地址*使用的参数[ **！ 分析-v** ](-analyze.md)命令。

**！ Cppexr**扩展可用于确定 c + + 异常的类型。

 

 





