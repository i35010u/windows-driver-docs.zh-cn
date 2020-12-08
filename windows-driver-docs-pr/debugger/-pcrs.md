---
title: pcrs
description: Pcrs 扩展显示 Intel Itanium 专用处理器控制寄存器。
keywords:
- " (PCR) 处理器控制寄存器"
- 'PCR (处理器控制寄存器) '
- pcrs Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pcrs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ef65e0e376f0548de1b8fb08974047b601c0c0f3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795727"
---
# <a name="pcrs"></a>!pcrs


**！ Pcrs** Extension 显示 Intel Itanium 专用处理器控制寄存器。

```dbgcmd
!pcrs Address
```

**重要提示**  此命令在 Windows 调试器版本10.0.14257 和更高版本中已弃用，不再可用。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定处理器控制寄存器文件的地址。

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

<a name="remarks"></a>备注
-------

不要将 **！ pcrs** 扩展与 [**！ pcr**](-pcr.md) 扩展相混淆，后者会显示处理器控件区域的当前状态。

 

 





