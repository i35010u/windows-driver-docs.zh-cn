---
title: cppexr
description: Cppexr 扩展显示 c + + 异常记录的内容。
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
ms.openlocfilehash: a73a2c4cd574f35c0e9e61bd86fa972c8db7d8c6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803337"
---
# <a name="cppexr"></a>!cppexr


**！ Cppexr** 扩展显示 c + + 异常记录的内容。

```dbgsyntax
    !cppexr Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示的 c + + 异常记录的地址。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关异常的详细信息，请参阅 Russinovich 和 David 所罗门群岛： [控制异常和事件](controlling-exceptions-and-events.md)、Windows 驱动程序工具包 (WDK) 文档、Windows SDK 文档和 *Microsoft Windows 内部机制* 。 使用 [**.exr**](-exr--display-exception-record-.md) 命令可以显示其他异常记录。

<a name="remarks"></a>备注
-------

**！ Cppexr** 扩展显示与目标遇到的 c + + 异常有关的信息，其中包括异常代码、异常的地址和异常标志。 此异常必须是 Msvcrt.dll 中定义的标准 c + + 异常之一。

通常可以使用 [**！分析-v**](-analyze.md)命令获取 *Address* 参数。

**！ Cppexr** 扩展适用于确定 c + + 异常的类型。

 

 





