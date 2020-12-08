---
title: .block
description: Block 标记不执行任何操作;它仅用于引入语句块。
keywords:
- 。阻止 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .block
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 15744264ec3a708e0445fd8767d1df35d4f35076
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799979"
---
# <a name="block"></a>.block


**Block** 标记不执行任何操作;它仅用于引入语句块。

```dbgcmd
    Commands ; .block { Commands } ; Commands 
```

## <span id="ddk_token_block_dbg"></span><span id="DDK_TOKEN_BLOCK_DBG"></span>


### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关使用新块来评估别名的信息，请参阅 [使用别名](using-aliases.md) 和 [**as，作为 (设置别名)**](as--as--set-alias-.md)。

有关其他控制流令牌及其在调试器命令程序中的使用的信息，请参阅 [使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

命令块用大括号括起来。 输入每个块后，将计算块中的所有别名。 如果在命令块中的某个时间点更改别名的值，则该点之后的命令将不会使用新的别名值，除非它们位于从属块内。

每个块必须以控制流令牌开头。 如果希望为计算别名的唯一目的创建一个块，则应将其作为 **块** 标记的前缀，因为除了允许引入块外，此标记不会有任何影响。

 

 





