---
title: 所有者
description: 所有者扩展显示的模块或函数的所有者。
ms.assetid: f881bd86-89cf-49fd-9bca-3ecc96123be8
keywords:
- Windows 调试的所有者
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- owner
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ad1f624edd930da5da8edc86ae1ab4b61d90d45e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334422"
---
# <a name="owner"></a>!owner


**！ 所有者**扩展显示的模块或函数的所有者。

```dbgcmd
!owner [Module[!Symbol]]
```

## <a name="span-idddkownerdbgspanspan-idddkownerdbgspanparameters"></a><span id="ddk__owner_dbg"></span><span id="DDK__OWNER_DBG"></span>参数


<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *模块*   
指定其所有者所需的模块。 一个星号 (\*) 的末尾*模块*表示任意数量的其他字符。

<span id="_______Symbol______"></span><span id="_______symbol______"></span><span id="_______SYMBOL______"></span> *符号*   
指定在符号*模块*所需的所有者。 一个星号 (\*) 的末尾*符号*表示任意数量的其他字符。 如果*符号*是省略，将显示整个模块的所有者。

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

 

<a name="remarks"></a>备注
-------

如果不使用任何参数，并且发生了错误，请 **！ 所有者**将显示出错模块或函数的所有者的名称。

当传递到模块或函数名称 **！ 所有者**扩展，调试器显示单词**跟进**跟指定的模块或函数的所有者的名称。

对于此扩展以显示有用的信息，您必须首先创建包含所有者名称的模块和函数的 triage.ini 文件。

有关 triage.ini 文件，并举例说明的详细信息 **！ 所有者**扩展，请参阅[指定的模块和函数所有者](specifying-module-and-function-owners.md)。

 

 





