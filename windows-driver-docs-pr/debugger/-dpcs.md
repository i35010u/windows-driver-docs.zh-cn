---
title: dpcs
description: Dpc 扩展显示指定的处理器的延缓的过程调用 (DPC) 队列。
ms.assetid: b5f71fb5-6fc7-4e8f-a439-1edb188e9876
keywords:
- DPC （延迟的过程调用）
- dpc Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dpcs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dc1ffa6bbcade69f9d94847b745790d4a4b34eda
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533945"
---
# <a name="dpcs"></a>!dpcs


**！ Dpc**扩展显示指定的处理器的延缓的过程调用 (DPC) 队列。

```dbgcmd
!dpcs [Processor]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *Processor*   
指定一个处理器。 如果*处理器*省略，则会显示所有处理器的 DPC 队列。

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
<td align="left"><p><strong>Windows XP</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows Server 2003 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

Dpc 有关的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

 

 





