---
title: （块分隔符）
description: 一对大括号 （） 用于围绕调试器命令程序内的语句块。
ms.assetid: 1391fa51-61ce-40e5-8bf5-b5a2215c2bd9
keywords:
- （块分隔符）Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Block Delimiter)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9f3cdd069ee946d32c692dbed305cd0ce3427b68
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334863"
---
# <a name="--block-delimiter"></a>{} （块分隔符）


对大括号 ( **{}** ) 用于围绕调试器命令程序内的语句块。

```dbgcmd
    Statements { Statements } Statements 
```

## <span id="ddk_token_block_delimiter_dbg"></span><span id="DDK_TOKEN_BLOCK_DELIMITER_DBG"></span>


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关调试器命令程序和控制流令牌的信息，请参阅[使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

输入每个块后，评估在块中的所有别名。 如果您更改的命令块中的某个时刻的别名值，该点之后的命令将不会使用新的别名值，除非它们是从属块内。

每个块必须以开头的控制流令牌。 如果你想要评估的别名的目的创建一个块，应将其与前缀[ **.block** ](-block.md)令牌。

 

 





