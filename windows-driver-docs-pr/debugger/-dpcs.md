---
title: 指
description: Dpc 扩展显示指定处理器 (DPC) 队列的延迟过程调用。
keywords:
- 'DPC (延迟的过程调用) '
- dpc Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dpcs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f07d6f60913d92e6e700aee641ae7d938d01ede0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816447"
---
# <a name="dpcs"></a>!dpcs


**！ Dpc** 扩展显示指定处理器 (DPC) 队列的延迟过程调用。

```dbgcmd
!dpcs [Processor]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*处理器*   
指定处理器。 如果省略了 *Processor* ，则显示所有处理器的 DPC 队列。

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
<td align="left"><p><strong>Windows XP</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows Server 2003 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 Dpc 的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部机制* ，Mark Russinovich 和 David 所罗门群岛。

 

 





