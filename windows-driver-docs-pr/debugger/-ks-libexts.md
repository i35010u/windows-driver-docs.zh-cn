---
title: ks. libexts
description: Libexts 扩展提供对以静态方式链接到扩展模块的 Microsoft 提供的库扩展的访问。
keywords:
- libexts Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.libexts
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2c8b9ff0634b3727e04f68a91b44d2100b15b132
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804073"
---
# <a name="kslibexts"></a>!ks.libexts


使用 **！ libexts** 扩展可以访问以静态方式链接到扩展模块的 Microsoft 提供的库扩展。

```dbgcmd
!ks.libexts [Command] [Libext] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="Command"></span><span id="command"></span><span id="COMMAND"></span>*Command*  
可选。 指定下列值之一。 如果省略此参数，则 **！ libexts** 返回帮助信息。

<span id="disableall________"></span><span id="DISABLEALL________"></span>**disableall**   
禁用所有库扩展。 如果使用此参数，则省略 *Libext* 参数。

<span id="_________disable"></span><span id="_________DISABLE"></span>**禁用**  
按名称禁用特定的库扩展。 如果使用此参数，请在 *Libext* 参数中指定该名称。

<span id="_________enableall"></span><span id="_________ENABLEALL"></span>**enableall**  
启用所有库扩展。 仅启用具有正确符号的已加载组件。 如果使用此参数，则省略 *Libext* 参数。

<span id="enable"></span><span id="ENABLE"></span>**可**  
按名称启用特定的库扩展。 如果使用此参数，请在 *Libext* 参数中指定该名称。 只能启用具有正确符号的已加载组件。

<span id="_________details"></span><span id="_________DETAILS"></span>**详细信息**  
显示有关当前链接的所有库扩展的详细信息。 如果使用此参数，则省略 *Libext* 参数。

<span id="_______Libext______"></span><span id="_______libext______"></span><span id="_______LIBEXT______"></span>*Libext*   
指定库扩展的名称。 仅对 **enable** 或 **disable** 的 *命令* 值是必需的。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [内核流调试](kernel-streaming-debugging.md)。

<a name="remarks"></a>备注
-------

扩展模块包含一个可扩展性框架，可用于生成单独的组件并将其链接到 Ks.dll。 这些额外的组件称为库扩展。

通过 **！ libexts** 命令，可以查看有关这些库扩展的统计信息并对其进行控制。 有关详细信息，请 **libexts** 不带参数的。

 

 





