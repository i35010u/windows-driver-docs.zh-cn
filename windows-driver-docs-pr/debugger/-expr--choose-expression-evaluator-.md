---
title: .expr（选择表达式评估器）
description: .Expr 命令指定默认表达式计算器。
ms.assetid: 96d246c2-10fe-4688-a04f-1325ac51e4b3
keywords:
- .expr （选择表达式计算器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .expr (Choose Expression Evaluator)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 54e745cb7c255e0503ce62f83f90c5b01e2c8693
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336770"
---
# <a name="expr-choose-expression-evaluator"></a>.expr（选择表达式评估器）


**.Expr**命令指定默认表达式计算器。

```dbgcmd
.expr /s masm 
.expr /s c++ 
.expr /q 
.expr 
```

## <a name="span-idddkmetachooseexpressionevaluatordbgspanspan-idddkmetachooseexpressionevaluatordbgspanparameters"></a><span id="ddk_meta_choose_expression_evaluator_dbg"></span><span id="DDK_META_CHOOSE_EXPRESSION_EVALUATOR_DBG"></span>参数


<span id="________s_masm______"></span><span id="________S_MASM______"></span> **/s masm**   
默认表达式类型更改为 Microsoft 组装器表达式计算器 (MASM)。 启动调试器时，此类型将是默认值。

<span id="________s_c________"></span><span id="________S_C________"></span> **/s c + +**   
更改默认表达式类型设置为C++表达式计算器。

<span id="________q______"></span><span id="________Q______"></span> **/q**   
显示可能的表达式类型的列表。

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

当你使用 **.expr**命令不带参数，则调试器会显示当前的默认表达式类型。

[ **??(评估C++表达式)** ](----evaluate-c---expression-.md)命令，监视窗口中，并[局部变量窗口](locals-window.md)始终使用C++表达式语法。 所有其他命令和信息的调试窗口使用默认表达式计算器。

有关如何控制使用哪种语法的详细信息，请参阅[评估表达式](evaluating-expressions.md)。 有关语法的详细信息，请参阅[数值表达式语法](numerical-expression-syntax.md)。

 

 





