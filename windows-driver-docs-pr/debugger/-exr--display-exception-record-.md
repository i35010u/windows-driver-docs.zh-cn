---
title: .exr（显示异常记录）
description: .Exr 命令显示异常记录的内容。
keywords:
- ) 命令 ( 显示异常记录
- 异常记录
- .exr (显示) Windows 调试的异常记录
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .exr (Display Exception Record)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e62c0aa4b2f2f6c9f9df8adfd7afdb0d6e2787aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820411"
---
# <a name="exr-display-exception-record"></a>.exr（显示异常记录）


**.Exr** 命令显示异常记录的内容。

```dbgcmd
.exr Address 
.exr -1
```

## <a name="span-idddk_meta_display_exception_record_dbgspanspan-idddk_meta_display_exception_record_dbgspanparameters"></a><span id="ddk_meta_display_exception_record_dbg"></span><span id="DDK_META_DISPLAY_EXCEPTION_RECORD_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定异常记录的地址。 如果将 **-1** 指定为地址，则调试器会显示最新的异常。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**.Exr** 命令显示与调试器在目标计算机上遇到的异常有关的信息。 显示的信息包括异常地址、异常代码、异常标志以及异常的参数的变量列表。

通常可以使用 [**！ pcr**](-pcr.md)扩展来获取 *地址*。

**.Exr** 命令通常用于调试 Bug 检查0x1E。 有关详细信息和示例，请参阅 [**Bug 检查 0x1E**](bug-check-0x1e--kmode-exception-not-handled.md) (\_ \_ 未 \_ 处理的 KMODE 异常) 。

 

 





