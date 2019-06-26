---
title: gle
description: Gle 扩展显示当前线程的最后一个错误值。
ms.assetid: bed3ce17-6860-421f-ae20-11faa50310ed
keywords:
- 线程，错误值
- 错误值
- gle Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gle
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cbb42db9d56bab021bd7f0a25194e31398110bbf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362495"
---
# <a name="gle"></a>!gle


**！ Gle**扩展显示当前线程的最后一个错误值。

```dbgcmd
!gle [-all]
```

## <a name="span-idddkgledbgspanspan-idddkgledbgspanparameters"></a><span id="ddk__gle_dbg"></span><span id="DDK__GLE_DBG"></span>参数


<span id="_______-all______"></span><span id="_______-ALL______"></span> **-all**   
在目标系统上显示每个用户模式线程的最后一个错误。 如果省略此参数在用户模式下，调试器会显示当前线程的最后一个错误。 如果省略此参数在内核模式下，调试器将显示线程的最后一个错误，当前[注册上下文](changing-contexts.md#register-context)指定。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Ext.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息[ **GetLastError** ](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror)例程，请参阅 Micorosft Windows SDK 文档。

<a name="remarks"></a>备注
-------

**！ Gle**扩展中显示的值[ **GetLastError** ](https://docs.microsoft.com/windows/desktop/api/errhandlingapi/nf-errhandlingapi-getlasterror)并尝试对此值进行解码。

在内核模式下 **！ gle**扩展工作仅当调试程序可以读取的线程环境块 (TEB)。

 

 





