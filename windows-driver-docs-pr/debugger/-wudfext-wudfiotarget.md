---
title: wudfext.wudfiotarget
description: Wudfext.wudfiotarget 扩展显示有关包括目标的状态和已发送请求的列表的 I/O 目标信息。
ms.assetid: ccd241d6-c9c8-4518-902c-f119cf5b73fe
keywords:
- wudfext.wudfiotarget Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfiotarget
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f4c50159c04826100e7e9fd6e36a3d8e5990731c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567301"
---
# <a name="wudfextwudfiotarget"></a>!wudfext.wudfiotarget


**！ Wudfext.wudfiotarget**扩展显示有关包括目标的状态和已发送请求的列表的 I/O 目标的信息。

```dbgcmd
!wudfext.wudfiotarget pWDFTarget TypeName
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______pWDFTarget______"></span><span id="_______pwdftarget______"></span><span id="_______PWDFTARGET______"></span> *pWDFTarget*   
指定的地址**IWDFIoTarget**接口来显示有关的信息。 [ **！ Wudfext.wudfobject** ](-wudfext-wudfobject.md)扩展命令确定地址**IWDFIoTarget**。

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

 

 





