---
title: cppexr
description: Cppexr 扩展显示C++异常记录的内容。
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
ms.openlocfilehash: ff22aa889368d13e27baa86891df6b2f32e298a1
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025273"
---
# <a name="cppexr"></a>!cppexr


**! Cppexr**扩展显示C++异常记录的内容。

```dbgsyntax
    !cppexr Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示的C++异常记录的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext .dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p>Ext .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关异常的详细信息, 请参阅 Russinovich 和 David 所罗门群岛:[控制异常和事件](controlling-exceptions-and-events.md)、Windows 驱动程序工具包 (WDK) 文档、Windows SDK 文档和*Microsoft Windows 内部机制*。 使用[ **.exr**](-exr--display-exception-record-.md)命令可以显示其他异常记录。

<a name="remarks"></a>备注
-------

**! Cppexr**扩展显示与目标遇到的C++异常有关的信息, 其中包括异常代码、异常的地址和异常标志。 此异常必须是 Msvcrt.lib 中定义的C++标准异常之一。

通常可以使用[ **! 分析-v**](-analyze.md)命令获取*Address*参数。

**! Cppexr**扩展适用于确定C++异常类型。

 

 





