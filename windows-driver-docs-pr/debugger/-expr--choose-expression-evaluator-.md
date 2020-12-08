---
title: .expr（选择表达式评估器）
description: Expr 命令指定默认表达式计算器。
keywords:
- expr (选择表达式计算器) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .expr (Choose Expression Evaluator)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5f8a3e48aa3835bd846d7467cb187eefaa4d210e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820413"
---
# <a name="expr-choose-expression-evaluator"></a>.expr（选择表达式评估器）


**Expr** 命令指定默认表达式计算器。

```dbgcmd
.expr /s masm 
.expr /s c++ 
.expr /q 
.expr 
```

## <a name="span-idddk_meta_choose_expression_evaluator_dbgspanspan-idddk_meta_choose_expression_evaluator_dbgspanparameters"></a><span id="ddk_meta_choose_expression_evaluator_dbg"></span><span id="DDK_META_CHOOSE_EXPRESSION_EVALUATOR_DBG"></span>参数


<span id="________s_masm______"></span><span id="________S_MASM______"></span>**/s masm**   
将默认表达式类型更改为 Microsoft 汇编程序 expression 计算器 (MASM) 。 启动调试器时，此类型为默认值。

<span id="________s_c________"></span><span id="________S_C________"></span>**/s c + +**   
将默认表达式类型更改为 c + + 表达式计算器。

<span id="________q______"></span><span id="________Q______"></span>**/q**   
显示可能的表达式类型的列表。

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

使用不带参数的 **expr** 命令时，调试器将显示当前的默认表达式类型。

" [**(" 计算 c + + 表达式)**](----evaluate-c---expression-.md) 命令、监视窗口和 " [局部变量" 窗口](locals-window.md) 始终使用 c + + 表达式语法。 所有其他命令和调试信息 windows 都使用默认表达式计算器。

有关如何控制所使用的语法的详细信息，请参阅 [计算表达式](evaluating-expressions.md)。 有关语法的详细信息，请参阅 [数值表达式语法](numerical-expression-syntax.md)。

 

 





