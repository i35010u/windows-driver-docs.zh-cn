---
title: cppexr
description: Cppexr 扩展显示的内容C++异常记录。
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
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336882"
---
# <a name="cppexr"></a>!cppexr


**！ Cppexr**扩展显示的内容C++异常记录。

```dbgsyntax
    !cppexr Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的地址的C++若要显示的异常记录。

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

**！ Cppexr**扩展插件都会显示为相关的信息，C++目标遇到，包括异常代码、 异常和异常标志的地址的异常。 此异常必须是一个标准C++在 Msvcrt.dll 中定义的异常。

通常可以获得*地址*使用的参数[ **！ 分析-v** ](-analyze.md)命令。

**！ Cppexr**扩展插件可用于确定的类型C++异常。

 

 





