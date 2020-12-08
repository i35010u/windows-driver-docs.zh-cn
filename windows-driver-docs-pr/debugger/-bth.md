---
title: bth
description: Bth 扩展为指定的处理器显示基于 Itanium 的分支跟踪历史记录。
keywords:
- 分支跟踪历史记录
- bth Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bth
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a291856f134df4bc2ff21d32f2a4ca9d417d7e55
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799943"
---
# <a name="bth"></a>!bth


**！ Bth** extension 为指定的处理器显示基于 Itanium 的分支跟踪历史记录。

```dbgcmd
!bth [Processor]
```

**重要提示**  此命令在 Windows 调试器版本10.0.14257 和更高版本中已弃用，不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*处理器*   
指定处理器。 如果省略了 *Processor* ，则显示所有处理器的分支跟踪历史记录。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

此扩展命令只能与基于 Itanium 的目标计算机一起使用。

 

 





