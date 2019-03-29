---
title: swd
description: Swd 扩展插件都会显示在指定的处理器，包括延迟的过程调用 (DPC) 和线程监视程序计时器状态的软件监视程序计时器状态。
ms.assetid: 03532c7e-3bfc-4e37-8a0a-0a7c5a9963a8
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
ms.openlocfilehash: b00f32e34ef8729dbd2f5a690d965c9113e49c68
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568202"
---
# <a name="swd"></a>!swd


**！ Swd**扩展插件都会显示在指定的处理器，包括延迟的过程调用 (DPC) 和线程监视程序计时器状态的软件监视程序计时器状态。

```dbgcmd
!swd [Processor]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *Processor*   
指定的处理器。 如果*处理器*是省略，目标计算机上的所有处理器的显示信息。

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

 

<a name="remarks"></a>备注
-------

监视程序计时器关闭或重新启动 Windows，如果 Windows 停止响应。 以秒为单位显示时间。

 

 





