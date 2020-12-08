---
title: （计算 C++ 表达式）
description: Double 问号 ( ) 命令根据 c + + 表达式规则计算并显示表达式的值。
keywords:
- " (在 Windows 调试) 计算 c + + 表达式"
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Evaluate C++ Expression)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6658a8e13623b0daed986f863d44c29bfcf09915
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800217"
---
# <a name="-evaluate-c-expression"></a>?? （计算 C++ 表达式）


Double 问号 (**？？**) 命令根据 c + + 表达式规则计算并显示表达式的值。

```dbgcmd
    ?? Expression
```

## <a name="span-idddk_cmd_evaluate_c_expression_dbgspanspan-idddk_cmd_evaluate_c_expression_dbgspanparameters"></a><span id="ddk_cmd_evaluate_c_expression_dbg"></span><span id="DDK_CMD_EVALUATE_C_EXPRESSION_DBG"></span>参数


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span>*表达式*   
指定要计算的 c + + 表达式。 有关语法的详细信息，请参阅 [c + + 编号和运算符](c---numbers-and-operators.md)。

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

**？？** 命令在当前线程和进程的上下文中计算表达式中的符号。

如果要根据 MASM 表达式规则来计算 **表达式** 表达式的一部分，请将该部分括在括号中，并在其前面添加两个 at 符号 ( **@@** ) 。 有关 MASM 表达式和 c + + 表达式的详细信息，请参阅 [计算表达式](evaluating-expressions.md) 和 [数值表达式语法](numerical-expression-syntax.md)。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**? (计算表达式)**](---evaluate-expression-.md)

[**.formats（显示数字格式）**](-formats--show-number-formats-.md)

 

 






