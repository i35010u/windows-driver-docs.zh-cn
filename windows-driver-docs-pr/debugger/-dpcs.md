---
title: 指
description: Dpc 扩展为指定的处理器显示延迟的过程调用 (DPC) 队列。
ms.assetid: b5f71fb5-6fc7-4e8f-a439-1edb188e9876
keywords:
- DPC (延迟过程调用)
- dpc Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dpcs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 79833c0723cf1c7a30ad8c0a03a1b8595e3031d8
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025269"
---
# <a name="dpcs"></a>!dpcs


**! Dpc** extension 为指定的处理器显示延迟的过程调用 (DPC) 队列。

```dbgcmd
!dpcs [Processor]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*处理器*   
指定处理器。 如果省略了*Processor* , 则显示所有处理器的 DPC 队列。

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
<td align="left"><p>Kdexts</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 Dpc 的信息, 请参阅 Windows 驱动程序工具包 (WDK) 文档和*Microsoft Windows 内部*Russinovich, 并将其标记为 "" 和 "David"。

 

 





