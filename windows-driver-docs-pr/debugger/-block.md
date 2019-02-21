---
title: .block
description: .Block 令牌不执行任何操作;它仅用于介绍语句块。
ms.assetid: 8f1ac6b5-fea5-4e3f-8d4c-5e0533722885
keywords:
- .block Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .block
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6e46ceb9218c59b605d7eb29ae2e14c486412cf8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547593"
---
# <a name="block"></a>.block


**.Block**令牌不执行任何操作; 它只用来引入语句块。

```dbgcmd
    Commands ; .block { Commands } ; Commands 
```

## <span id="ddk_token_block_dbg"></span><span id="DDK_TOKEN_BLOCK_DBG"></span>


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关使用新的块评估别名的信息，请参阅[Using 别名](using-aliases.md)并[**一样 （设置别名） 作为**](as--as--set-alias-.md)。

有关其他控制流令牌在调试器命令程序及其用法的信息，请参阅[使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

命令块括在大括号。 输入每个块后，评估在块中的所有别名。 如果您更改的命令块中的某个时刻的别名值，该点之后的命令将不会使用新的别名值，除非它们是从属块内。

每个块必须以开头的控制流令牌。 如果你想要评估的别名的目的创建一个块，应将其与前缀 **.block**令牌，因为此令牌不起作用而不允许的块，将会推出。

 

 





