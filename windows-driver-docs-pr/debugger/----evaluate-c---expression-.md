---
title: （计算 C++ 表达式）
description: 双精度问号 （） 命令的计算结果并显示根据表达式的值C++表达式规则。
ms.assetid: 3a15a0a3-03d0-4807-a6df-054de819c0a0
keywords:
- (评估C++表达式)Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Evaluate C++ Expression)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d87d24430baa315e9e0ec45fdbdb21eb441f76ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334858"
---
# <a name="-evaluate-c-expression"></a>?? （计算 C++ 表达式）


双精度问号 (**??**) 命令的计算结果并显示根据表达式的值C++表达式规则。

```dbgcmd
    ?? Expression
```

## <a name="span-idddkcmdevaluatecexpressiondbgspanspan-idddkcmdevaluatecexpressiondbgspanparameters"></a><span id="ddk_cmd_evaluate_c_expression_dbg"></span><span id="DDK_CMD_EVALUATE_C_EXPRESSION_DBG"></span>参数


<span id="_______Expression______"></span><span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *表达式*   
指定C++要计算的表达式。 有关语法的详细信息，请参阅[C++数字和运算符](c---numbers-and-operators.md)。

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

**??** 命令可评估当前的线程和进程的上下文中的表达式中的符号。

如果你想要评估的一部分**表达式**根据 MASM 表达式规则的表达式将该部分括在括号中，添加两个 at 符号 ( **@@** ) 之前。 MASM 表达式有关的详细信息和C++表达式，请参阅[评估表达式](evaluating-expressions.md)并[数值表达式语法](numerical-expression-syntax.md)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**?（计算表达式）**](---evaluate-expression-.md)

[**.formats （显示数字格式）**](-formats--show-number-formats-.md)

 

 






