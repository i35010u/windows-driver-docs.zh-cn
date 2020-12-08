---
title: " (块分隔符) "
description: 一对大括号 ( ) 用于在调试器命令程序中包围语句块。
keywords:
- " (块分隔符) Windows 调试"
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Block Delimiter)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 52e7f42ec55b852a01ebcc6096eed634f2b9fb28
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800233"
---
# <a name="--block-delimiter"></a>{} (阻止分隔符) 


一对大括号 ( **{}** ) 用于在调试器命令程序中包围语句块。

```dbgcmd
    Statements { Statements } Statements 
```

## <span id="ddk_token_block_delimiter_dbg"></span><span id="DDK_TOKEN_BLOCK_DELIMITER_DBG"></span>


### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关调试器命令程序和控制流令牌的信息，请参阅 [使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

输入每个块后，将计算块中的所有别名。 如果在命令块中的某个时间点更改别名的值，则该点之后的命令将不会使用新的别名值，除非它们位于从属块内。

每个块必须以控制流令牌开头。 如果希望为计算别名的唯一目的创建一个块，则应将其作为 [**块**](-block.md) 标记的前缀。

 

 





