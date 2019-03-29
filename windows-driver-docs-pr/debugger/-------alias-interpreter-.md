---
title: $ （别名解释器）
description: 美元符号后跟一对大括号 （$） 的计算结果为各种与指定的用户命名别名相关的值。
ms.assetid: 5182ed99-259e-4e58-8d69-38a702bd8113
keywords:
- $ （别名解释器） Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- $ (Alias Interpreter)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ebf7173cffb7a3fed01c4e06a97e3ed8529d1c8d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569084"
---
# <a name="--alias-interpreter"></a>$ {} （别名解释器）


美元符号后跟一对括号 ( **$ {}** ) 的计算结果为各种与指定的用户命名别名相关的值。

```dbgcmd

    Text ${Alias} Text 
    Text ${/d:Alias} Text 
    Text ${/f:Alias} Text 
    Text ${/n:Alias} Text 
    Text ${/v:Alias} Text 
```

## <a name="span-idddktokenaliasinterpreterdbgspanspan-idddktokenaliasinterpreterdbgspanparameters"></a><span id="ddk_token_alias_interpreter_dbg"></span><span id="DDK_TOKEN_ALIAS_INTERPRETER_DBG"></span>参数


<span id="Alias"></span><span id="alias"></span><span id="ALIAS"></span>*别名*  
指定要展开或计算的别名的名称。 *别名*必须是用户命名别名或*变量*使用值[ **.foreach** ](-foreach.md)令牌。

<span id="_d"></span><span id="_D"></span>**/d**  
计算结果为一个或零个具体情况取决于是否当前定义别名。 如果定义别名，则 **${/ v 部分：**<em>别名</em>**}** 替换为 1; 如果未定义别名， **${/ v 部分：**<em>别名</em>**}** 替换为 0。

<span id="_f"></span><span id="_F"></span>**/f**  
如果当前定义别名的计算结果为等效的别名。 如果定义别名，则 **${/ f:**<em>别名</em>**}** 如果未定义别名，将替换为等效的别名; **${/ f:** <em>别名</em>**}** 替换为空字符串。

<span id="_n"></span><span id="_N"></span>**/n**  
如果当前定义的别名，计算结果的别名名称。 如果定义别名，则 **${/ n:**<em>别名</em>**}** 被替换为别名名称; 如果未定义别名， **${/ n:** <em>别名</em>**}** 不会被替换，但保留其文本值 **${/ n:**<em>别名</em>**}**。

<span id="_v"></span><span id="_V"></span>**/v**  
可以防止任何别名评估。 无论是否*别名*定义，则 **${/ v 部分：**<em>别名</em>**}** 始终保留其文本值 **${/ v 部分：** <em>别名</em>**}**。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关如何使用别名的说明，请参阅[Using 别名](using-aliases.md)。

<a name="remarks"></a>备注
-------

如果不使用任何开关，并且当前定义别名， **${**<em>别名</em>**}** 替换为等效的别名。 如果不使用任何开关，并且未定义别名，则 **${**<em>别名</em>**}** 始终保留其文本值 **${** <em>别名</em>**}**。

使用的一个优点 **$ {}** 令牌是即使它是相邻的其他字符，将评估该别名。 没有此令牌，调试器仅替换从其他令牌由空格分隔的别名。

如所述，一些情况其中 **$ {}** 令牌不会被替换的任何内容，但会保留其文本值。 发生这种情况是如果不使用任何开关和*别名*未定义，当 **/n**使用开关和*别名*未定义，和时始终 **/v**使用开关。 在这些情况下，令牌会保留其文本值，包括美元符号和大括号。 因此，如果这使用作为命令的参数，语法会导致错误，除非该参数接受任意文本字符串。

没有，但是，一个例外。 如果您使用 **${/ v 部分：**<em>别名</em>**}** 作为第一个参数[ **（设置别名） 作为**](as--as--set-alias-.md)或 **（设置别名） 作为**命令时，此令牌将被视为字符串*别名*不作为字符串单独 **${/ v 部分：**<em>别名</em>**}**. 这仅适用于**作为**，**作为**，并**ad**命令，也时才起作用 **/v**使用开关，它不会使用 **${/ n:**<em>别名</em>**}** 或者 **${**<em>别名</em>**}** 时它们保留其文本值。

*别名*必须是用户命名别名或*变量*使用值[ **.foreach** ](-foreach.md)令牌-未固定名称别名。 如果没有在字符串中的固定名称别名*别名*，将其替换之前 **$ {}** 计算令牌。

 

 





