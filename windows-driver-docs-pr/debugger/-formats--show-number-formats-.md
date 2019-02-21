---
title: .formats （显示数字格式）
description: .Formats 命令的表达式或符号在当前线程和进程的上下文中的计算结果，并将其显示在多个数字的格式。
ms.assetid: 9eac92b3-5137-4adb-a074-31510dc9bff7
keywords:
- .formats （显示数字格式） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .formats (Show Number Formats)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 11a836c5c1dca791b17d16c5bee08f0e1e0dc5dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547619"
---
# <a name="formats-show-number-formats"></a>.formats （显示数字格式）


**.Formats**命令的表达式或符号在当前线程和进程的上下文中的计算结果并将其显示在多个数字的格式。

```dbgcmd
.formats expression 
```

## <a name="span-idddkmetashownumberformatsdbgspanspan-idddkmetashownumberformatsdbgspanparameters"></a><span id="ddk_meta_show_number_formats_dbg"></span><span id="DDK_META_SHOW_NUMBER_FORMATS_DBG"></span>参数


<span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *expression*   
指定要计算的表达式。 有关语法的详细信息，请参阅[数值表达式语法](numerical-expression-syntax.md)。

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

表达式的计算结果显示在十六进制、 十进制、 八进制和二进制格式，以及单精度和双精度浮点格式。 当字节对应标准 ASCII 字符时，也会显示 ASCII 字符格式。 如果在允许范围内，表达式还被解释为时间戳。

下面的示例演示 **.formats**命令。

```dbgcmd
0:000> .formats 1c407e62
Evaluate expression:
  Hex:     1c407e62
  Decimal: 473988706
  Octal:   03420077142
  Binary:  00011100 01000000 01111110 01100010
  Chars:   .@~b
  Time:    Mon Jan 07 15:31:46 1985
  Float:   low 6.36908e-022 high 0
  Double:  2.34182e-315
```

**时间**字段 CRT 的时间戳格式显示 32 位值，并以 FILETIME 格式显示 64 位值。 因为 FILETIME 格式包含毫秒，CRT 格式却没有，你可以区分这些格式。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**?（计算表达式）**](---evaluate-expression-.md)

[**??（计算结果 c + + 表达式）**](----evaluate-c---expression-.md)

 

 






