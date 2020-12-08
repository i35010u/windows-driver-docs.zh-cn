---
title: '$ (别名解释器) '
description: 后跟一对大括号的美元符号 ( $ ) 计算为与指定的用户命名别名相关的各种值。
keywords:
- $ (别名解释器) Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- $ (Alias Interpreter)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 043ae661a63321afd2bc0edab67068fee7627aed
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800235"
---
# <a name="--alias-interpreter"></a>$ {} (别名解释器) 


后跟一对大括号的美元符号 ( **$ {}** ) 计算为与指定的用户命名别名相关的各种值。

```dbgcmd

    Text ${Alias} Text 
    Text ${/d:Alias} Text 
    Text ${/f:Alias} Text 
    Text ${/n:Alias} Text 
    Text ${/v:Alias} Text 
```

## <a name="span-idddk_token_alias_interpreter_dbgspanspan-idddk_token_alias_interpreter_dbgspanparameters"></a><span id="ddk_token_alias_interpreter_dbg"></span><span id="DDK_TOKEN_ALIAS_INTERPRETER_DBG"></span>参数


<span id="Alias"></span><span id="alias"></span><span id="ALIAS"></span>*A*  
指定要扩展或计算的别名的名称。 *别名* 必须是用户命名的别名或 [**foreach**](-foreach.md)标记使用的 *变量* 值。

<span id="_d"></span><span id="_D"></span>**/d**  
计算结果为一或零，具体取决于当前是否定义了别名。 如果定义了别名，则 **$ {/v：**<em>alias</em>**}** 将替换为 1;如果未定义别名， **$ {/v：**<em>alias</em>**}** 将替换为0。

<span id="_f"></span><span id="_F"></span>**/f**  
如果当前定义了别名，则计算结果为等效的别名。 如果定义了别名，则 **$ {/f：**<em>alias</em>**}** 将替换为等效的别名;如果未定义别名，则将 **$ {/f：**<em>alias</em>**}** 替换为空字符串。

<span id="_n"></span><span id="_N"></span>**/n**  
如果当前定义了别名，则计算结果为别名。 如果定义了别名，则 **$ {/n：**<em>alias</em>**}** 将替换为别名;如果未定义别名，则不会替换 **$ {/n：**<em>alias</em>**}** ，而是保留其文本值 **$ {/n：**<em>alias</em>**}**。

<span id="_v"></span><span id="_V"></span>**/v**  
阻止任何别名评估。 不管是否定义了 *别名* ， **$ {/v：**<em>alias</em>**}** 始终保留其文本值 **$ {/v：**<em>alias</em>**}**。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何使用别名的说明，请参阅 [使用别名](using-aliases.md)。

<a name="remarks"></a>备注
-------

如果未使用任何开关，并且当前定义了别名，则 **$ {**<em>alias</em>**}** 将替换为等效的别名。 如果未使用任何开关，并且未定义别名， **$ {**<em>alias</em>**}** 始终保留其文本值 " **$ {**<em>alias</em>**}**"。

使用 **$ {}** 标记的一个优点是，即使别名与其他字符相邻，也会对其进行评估。 如果没有此标记，调试器将只替换由空格分隔的别名。

如所示，在某些情况下， **$ {}** 标记不会替换为任何内容，而是保留其文本值。 如果使用了 **/n** *开关并且未* 定义 *别名，* 并且在使用了 **/v** 开关时始终出现错误，则会发生这种情况。 在这些情况下，令牌保留其文本值，包括美元符号和大括号。 因此，如果将它用作命令的参数，将导致语法错误，除非该参数接受任意文本字符串。

但有一个例外。 如果使用 **$ {/v：**<em>Alias</em>**}** 作为 [**作为 (设置别名)**](as--as--set-alias-.md) 的第一个参数，或者使用 **(设置别名)** 命令，则此令牌将仅被视为字符串 *别名* ，而不是作为字符串 **$ {/v：**<em>Alias</em>**}**。 这仅适用于 **as**、 **as** 和 **ad** 命令，并且仅当使用了 **/v** 开关时才起作用，当用户保留其文本值时，它将不能与 **$ {/n：**<em>Alias</em>**}** 或 **$ {**<em>Alias</em>**}** 一起使用。

*别名* 必须是用户命名的别名或 [**foreach**](-foreach.md)标记使用的 *变量* 值，而不能是固定名称的别名。 如果字符串 *别名* 中有一个固定名的别名，则在对 **$ {}** 标记进行计算之前将替换它。

 

 





