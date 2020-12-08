---
title: .formats（显示数字格式）
description: Formats 命令在当前线程的上下文中计算表达式或符号，并处理并将其显示为多个数字格式。
keywords:
- . 格式 (显示数字格式) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .formats (Show Number Formats)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b20dc2524a253faa3f1f261afaf4be9de14545e6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822647"
---
# <a name="formats-show-number-formats"></a>.formats（显示数字格式）


**Formats** 命令在当前线程的上下文中计算表达式或符号，并处理并将其显示为多个数字格式。

```dbgcmd
.formats expression 
```

## <a name="span-idddk_meta_show_number_formats_dbgspanspan-idddk_meta_show_number_formats_dbgspanparameters"></a><span id="ddk_meta_show_number_formats_dbg"></span><span id="DDK_META_SHOW_NUMBER_FORMATS_DBG"></span>参数


<span id="_______expression______"></span><span id="_______EXPRESSION______"></span>*表达式*   
指定要计算的表达式。 有关语法的详细信息，请参阅 [数值表达式语法](numerical-expression-syntax.md)。

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

计算后的表达式显示为十六进制、十进制、八进制和二进制格式，以及单精度和双精度浮点格式。 当字节对应于标准 ASCII 字符时，还会显示 ASCII 字符格式。 如果表达式在允许的范围内，还会将其解释为时间戳。

下面的示例演示了 **formats** 命令。

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

" **时间** " 字段以 CRT 时间戳格式显示32位值，并以 FILETIME 格式显示64位值。 可以区分这些格式，因为 FILETIME 格式包括毫秒，而 CRT 格式不包含毫秒。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**? (计算表达式)**](---evaluate-expression-.md)

[**?? (评估 c + + 表达式)**](----evaluate-c---expression-.md)

 

 






