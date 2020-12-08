---
title: owner
description: 所有者扩展显示模块或函数的所有者。
keywords:
- 所有者 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- owner
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c2c1c2c6eaad838c654673ff91791f05c14213fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811255"
---
# <a name="owner"></a>!owner


**！ Owner** extension 显示模块或函数的所有者。

```dbgcmd
!owner [Module[!Symbol]]
```

## <a name="span-idddk__owner_dbgspanspan-idddk__owner_dbgspanparameters"></a><span id="ddk__owner_dbg"></span><span id="DDK__OWNER_DBG"></span>参数


<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span>*模块*   
指定需要其所有者的模块。 \**模块* 末尾)  (星号表示任意数量的附加字符。

<span id="_______Symbol______"></span><span id="_______symbol______"></span><span id="_______SYMBOL______"></span>*符号*   
指定需要其所有者的 *模块* 内的符号。 \**符号* 末尾)  (星号表示任意数量的其他字符。 如果省略 *符号* ，则显示整个模块的所有者。

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

 

<a name="remarks"></a>备注
-------

如果未使用任何参数并且发生错误，则 **！所有者** 将显示出错模块或函数的所有者的名称。

当您将模块或函数名称传递到 **！所有者** 扩展时，调试器将显示 " **后续** 单词后跟指定模块或函数的所有者的名称。

为了使此扩展显示有用信息，你必须首先创建一个 triage.ini 文件，其中包含模块和函数所有者的名称。

有关 triage.ini 文件和 **！所有者** 扩展的示例的详细信息，请参阅 [指定模块和函数所有者](specifying-module-and-function-owners.md)。

 

 





