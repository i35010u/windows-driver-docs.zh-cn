---
title: wudfext.wudfusbpipe
description: Wudfext.wudfusbpipe 扩展显示有关 USB 的管道对象的信息。
ms.assetid: a80f01e1-9c2c-4674-a067-0ff7e006713a
keywords:
- wudfext.wudfusbpipe Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfusbpipe
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 402dbbb3169cccf0121a06d227669b0d1f965a6b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351527"
---
# <a name="wudfextwudfusbpipe"></a>!wudfext.wudfusbpipe


**！ Wudfext.wudfusbpipe**扩展显示有关 USB 的管道对象的信息。

```dbgcmd
!wudfext.wudfusbpipe pWDFUSBPipe TypeName
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______pWDFUSBPipe______"></span><span id="_______pwdfusbpipe______"></span><span id="_______PWDFUSBPIPE______"></span> *pWDFUSBPipe*   
指定的地址**IWDFUsbTargetPipe**接口来显示有关的信息。 [ **！ Wudfext.wudfobject** ](-wudfext-wudfobject.md)扩展命令确定地址**IWDFUsbTargetPipe**。

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

 

 





