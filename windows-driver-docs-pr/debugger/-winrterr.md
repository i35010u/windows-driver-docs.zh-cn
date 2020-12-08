---
title: winrterr
description: Winrterr 为 Windows 运行时错误设置调试器报告模式。
keywords:
- winrterr Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- winrterr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 29c92c005a6e37f6ad73df45d5edb8e8ab06b260
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823565"
---
# <a name="winrterr"></a>!winrterr


**！ Winrterr** 为 Windows 运行时错误设置调试器报告模式。

```dbgcmd
!winrterr Mode
!winrterr
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="Mode"></span><span id="mode"></span><span id="MODE"></span>*众*  
下表描述了 *模式* 的可能值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="report"></span><span id="REPORT"></span>报表</p></td>
<td align="left"><p>发生 Windows 运行时错误时，错误和相关文本将显示在调试器中，但执行 contunues。 这是默认模式。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="break"></span><span id="BREAK"></span>分</p></td>
<td align="left"><p>发生 Windows 运行时错误时，错误和相关文本将显示在调试器中，并且执行将停止。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="quiet"></span><span id="QUIET"></span>低温</p></td>
<td align="left"><p>发生 Windows 运行时错误时，调试器中将不会显示任何内容，并且继续执行。</p></td>
</tr>
</tbody>
</table>

 

如果省略 *模式* ， **！ winrterr** 显示当前报告模式。 如果调试器由于 Windows 运行时错误而发生了损坏，也会显示错误和相关文本。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[Windows 运行时调试程序命令](windows-runtime-debugger-commands.md)

[**!hstring**](-hstring.md)

[**!hstring2**](-hstring2.md)

 

 






