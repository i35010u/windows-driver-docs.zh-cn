---
title: 星号字符注释行说明符
description: 如果星号字符位于命令的开头，则该行的其余部分将被视为注释，即使其后出现分号也是如此。
ms.assetid: 46f68e92-0758-49f2-82bb-bc4d25ddb641
keywords:
- 注释行标记
- 注释行说明符 Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- (Comment Line Specifier)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3572a854051b602196009ec38d74ed1c2d0e0d19
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038042"
---
# <a name="-comment-line-specifier"></a>\* （注释行说明符）

如果星号（ **\*** ）字符位于命令开头，则该行的其余部分将被视为注释，即使其后出现分号也是如此。

```dbgcmd
    * [any text]
```

<a name="remarks"></a>备注
-------

**@No__t**的令牌与任何其他调试器命令一样进行分析。 因此，如果要在另一个命令后创建注释，则必须在 **\*** 标记前面加上一个分号。

**@No__t-1**标记将导致行的其余部分被忽略，即使其后出现分号也是如此。 这不同于[ **$ $ （Comment 说明符）** ](-----comment-specifier-.md)，后者创建一个可由分号终止的注释。

例如，以下命令将显示**eax**和**ebx**，但不显示**ecx**：

```console
0:000> r eax; $$ some text; r ebx; * more text; r ecx
```

不会以任何方式处理 **\*** 或[ **$$** ](-----comment-specifier-.md)标记前面的文本。 如果要执行远程调试，则在调试服务器中输入的注释将在调试客户端中不可见，反之亦然。 如果希望使注释文本在调试器中出现命令窗口以对所有参与方可见的方式显示，则应使用[**echo （回显注释）** ](-echo--echo-comment-.md)。
