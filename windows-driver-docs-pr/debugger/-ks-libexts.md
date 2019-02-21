---
title: ks.libexts
description: Ks.libexts 扩展提供访问的静态链接到了扩展模块的 Microsoft 提供的库扩展。
ms.assetid: 03328041-9922-4367-b6e9-d822a9c03f32
keywords:
- ks.libexts Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.libexts
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 05c2e88f471b2aafa8b82a7d451103a5dcb130fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519895"
---
# <a name="kslibexts"></a>!ks.libexts


**！ Ks.libexts**扩展提供访问的静态链接到了扩展模块的 Microsoft 提供的库扩展。

```dbgcmd
!ks.libexts [Command] [Libext] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="Command"></span><span id="command"></span><span id="COMMAND"></span>*命令*  
可选。 指定以下值之一。 如果省略此参数，则 **！ ks.libexts**返回的帮助信息。

<span id="disableall________"></span><span id="DISABLEALL________"></span>**disableall**   
禁用库的所有扩展。 这使用时，省略*Libext*参数。

<span id="_________disable"></span><span id="_________DISABLE"></span> **disable**  
通过名称来禁用特定库扩展插件。 这使用时，指定在名称*Libext*参数。

<span id="_________enableall"></span><span id="_________ENABLEALL"></span> **enableall**  
启用库的所有扩展。 仅启用与正确的符号加载的组件。 这使用时，省略*Libext*参数。

<span id="enable"></span><span id="ENABLE"></span>**enable**  
启用特定库扩展插件的名称。 这使用时，指定在名称*Libext*参数。 仅可以启用与正确的符号加载的组件。

<span id="_________details"></span><span id="_________DETAILS"></span> **详细信息**  
显示有关当前链接的库的所有扩展的详细信息。 这使用时，省略*Libext*参数。

<span id="_______Libext______"></span><span id="_______libext______"></span><span id="_______LIBEXT______"></span> *Libext*   
指定库扩展插件的名称。 仅为所需*命令*的值**启用**或**禁用**。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[流式处理的内核调试](kernel-streaming-debugging.md)。

<a name="remarks"></a>备注
-------

扩展模块包含允许单独的组件以进行生成和链接到 Ks.dll 的可扩展性框架。 这些额外的组件称为库扩展插件。

**！ Ks.libexts**命令允许查看有关这些库扩展以及对其进行控制的统计信息。 有关详细信息，发出 **！ ks.libexts**不带任何参数。

 

 





