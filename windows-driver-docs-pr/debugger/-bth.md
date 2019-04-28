---
title: 同时为
description: 同时为扩展显示在指定的处理器的基于 Itanium 的分支跟踪历史记录。
ms.assetid: e6bf1452-adb7-4b1d-8614-03fcf0306c70
keywords:
- 分支跟踪历史记录
- 同时为 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bth
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8ebd4dcb2eacbf5d58fec19048bad1b912bd1267
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334666"
---
# <a name="bth"></a>!bth


**！ 同时为**扩展插件都会显示在指定的处理器的基于 Itanium 的分支跟踪历史记录。

```dbgcmd
!bth [Processor]
```

**重要**  此命令已被 Windows 调试器版本 10.0.14257 中不推荐使用和更高版本，并不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *Processor*   
指定一个处理器。 如果*处理器*省略，则显示所有处理器的分支跟踪历史记录。

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
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

此扩展命令仅用于基于 Itanium 的目标计算机。

 

 





