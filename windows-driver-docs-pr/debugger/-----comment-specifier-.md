---
title: $ $ （备注说明符）
description: 如果在命令开头出现两个美元符号（$ $），则该行的其余部分将被视为注释，除非注释以分号结束。
ms.assetid: bafd5e97-d443-4bfc-b3ee-c2867ed139a2
keywords:
- 注释标记（$ $）
- $ $ （注释说明符） Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- $$ (Comment Specifier)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d666b934c787f2f752bec83b97f9c4234db5a0f9
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038049"
---
# <a name="-comment-specifier"></a>$ $ （备注说明符）


如果在命令开头出现两个美元符号（ **$$** ），则该行的其余部分将被视为注释，除非注释以分号结束。


   $ $ [任意文本]


<a name="remarks"></a>备注
-------

**@No__t**的令牌与任何其他调试器命令一样进行分析。 因此，如果要在另一个命令后创建注释，则必须在 **$$** 标记前面加上一个分号。

**@No__t**的令牌将导致文本被忽略，直到到达行尾或遇到分号为止。 分号终止注释;分号后的文本将被分析为标准命令。 这不同于 **\*** [（注释行说明符）](----comment-line-specifier-.md) ，这会使行的其余部分成为注释（即使存在分号）。

例如，以下命令将显示**eax**和**ebx**，但不显示**ecx**：

```console
0:000> r eax; $$ some text; r ebx; * more text; r ecx 
```

不会以任何方式处理 **\*** 或 **$$** 标记前面的文本。 如果要执行远程调试，则在调试服务器中输入的注释将在调试客户端中不可见，反之亦然。 如果希望使注释文本在调试器中出现命令窗口以对所有参与方可见的方式显示，则应使用[**echo （回显注释）** ](-echo--echo-comment-.md)。
