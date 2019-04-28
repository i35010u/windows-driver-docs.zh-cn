---
title: winrterr
description: Winrterr 设置调试器报告模式下的 Windows 运行时错误。
ms.assetid: 72E3EF7A-6055-405F-9E24-C9B81C07B8A7
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
ms.openlocfilehash: c9ad1fceba52fcf3c86a75e865cc605ed8649d3e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343155"
---
# <a name="winrterr"></a>!winrterr


**！ Winrterr**设置调试器报告模式下的 Windows 运行时错误。

```dbgcmd
!winrterr Mode
!winrterr
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="Mode"></span><span id="mode"></span><span id="MODE"></span>*模式*  
下表描述了可能的值为*模式下*。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="report"></span><span id="REPORT"></span>report</p></td>
<td align="left"><p>Windows 运行时错误时，调试器，但执行 contunues 中显示的错误和相关的文本。 此为默认模式。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="break"></span><span id="BREAK"></span>break</p></td>
<td align="left"><p>Windows 运行时错误时，错误和相关的文本显示在调试器中，并且停止执行。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="quiet"></span><span id="QUIET"></span>quiet</p></td>
<td align="left"><p>当发生 Windows 运行时错误，不会显示在调试器中，并继续执行。</p></td>
</tr>
</tbody>
</table>

 

如果*模式下*省略，则 **！ winrterr**显示当前报告模式。 如果在调试器由于 Windows 运行时错误而损坏，也会显示错误和相关的文本。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[Windows 运行时调试器命令](windows-runtime-debugger-commands.md)

[**!hstring**](-hstring.md)

[**!hstring2**](-hstring2.md)

 

 






