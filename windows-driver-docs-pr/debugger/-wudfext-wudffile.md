---
title: wudfext.wudffile
description: Wudfext.wudffile 扩展显示有关 framework 文件的信息。
ms.assetid: f655703d-0e61-4e9c-a033-834a89ef6d05
keywords:
- wudfext.wudffile Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudffile
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 19d7a0227b321310c8a00c0c98c923699ac51ad2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544102"
---
# <a name="wudfextwudffile"></a>!wudfext.wudffile


**！ Wudfext.wudffile**扩展显示框架文件有关的信息。

```dbgcmd
!wudfext.wudffile pWDFFile [TypeName] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______pWDFFile______"></span><span id="_______pwdffile______"></span><span id="_______PWDFFILE______"></span> *pWDFFile*   
指定的地址**IWDFFile**接口来显示有关的信息。

<span id="_______TypeName______"></span><span id="_______typename______"></span><span id="_______TYPENAME______"></span> *TypeName*   
可选。 指定的接口类型 (例如， **IWDFDevice**)。 如果为值*TypeName*是提供，该扩展使用的值作为接口的类型。 如果星号 (\*) 作为提供*TypeName*，或者如果*TypeName*是省略，该扩展会尝试自动确定提供的接口的类型。

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
<td align="left"><p><strong>使用 UMDF 1.7 和更高版本的 Windows XP</strong></p></td>
<td align="left"><p>Wudfext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

 

 





