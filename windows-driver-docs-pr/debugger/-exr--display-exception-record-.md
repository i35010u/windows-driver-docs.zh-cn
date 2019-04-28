---
title: .exr（显示异常记录）
description: .Exr 命令显示异常记录的内容。
ms.assetid: 786d7ee0-45d7-489c-b53b-28349ea10e36
keywords:
- 显示异常记录 (.exr) 命令
- 异常记录
- .exr （显示异常记录） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .exr (Display Exception Record)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3acae875f16df0a2d1c2517bc31d1c005c73119e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336754"
---
# <a name="exr-display-exception-record"></a>.exr（显示异常记录）


**.Exr**命令将显示异常记录的内容。

```dbgcmd
.exr Address 
.exr -1
```

## <a name="span-idddkmetadisplayexceptionrecorddbgspanspan-idddkmetadisplayexceptionrecorddbgspanparameters"></a><span id="ddk_meta_display_exception_record_dbg"></span><span id="DDK_META_DISPLAY_EXCEPTION_RECORD_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的异常记录的地址。 如果指定**为-1**作为地址，则调试器会显示最新的异常。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**.Exr**命令将显示与目标计算机的调试器遇到异常相关的信息。 显示的信息包括异常地址、 异常代码、 异常标志和对异常的参数的变量列表。

通常可以获得*地址*通过使用[ **！ pcr** ](-pcr.md)扩展。

**.Exr**命令通常用于调试 bug 检查 0x1E。 有关详细信息和示例，请参阅[ **Bug 检查 0x1E** ](bug-check-0x1e--kmode-exception-not-handled.md) (KMODE\_异常\_不\_HANDLED)。

 

 





