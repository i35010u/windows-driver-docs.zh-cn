---
title: swd
description: Swd 扩展显示指定处理器的软件监视程序计时器状态，包括延迟的过程调用 (DPC) 和线程的监视器计时器状态。
keywords:
- 监视程序计时器
- swd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- swd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 785ae834923745cea2b29aed1317f68d001974f0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824385"
---
# <a name="swd"></a>!swd


**！ Swd** extension 显示指定处理器的软件监视程序计时器状态，包括延迟的过程调用 (DPC) 和线程的监视器计时器状态。

```dbgcmd
!swd [Processor]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*处理器*   
指定处理器。 如果省略了 *Processor* ，则显示目标计算机上的所有处理器的信息。

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

 

<a name="remarks"></a>备注
-------

如果 Windows 停止响应，监视计时器会关闭或重新启动 Windows。 时间以秒为单位显示。

 

 





