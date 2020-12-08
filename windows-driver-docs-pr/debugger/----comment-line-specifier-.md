---
title: 星号字符注释行说明符
description: 如果星号字符位于命令的开头，则该行的其余部分将被视为注释，即使其后出现分号也是如此。
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
ms.openlocfilehash: eb8534f276aae228e29fbf07ba6a5dd4a768994d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800219"
---
# <a name="-comment-line-specifier"></a>\* (注释行说明符) 

如果星号 ( * *\** _ ) 字符位于命令开头，则该行的其余部分将被视为注释，即使其后出现分号也是如此。

```dbgcmd
    _ [any text]
```

<a name="remarks"></a>备注
-------

* *\** _ 标记的分析方式与任何其他调试器命令类似。 因此，如果要在另一个命令后创建注释，则必须在令牌前面加上 _*\**_ 一个分号。

_*\**_ 即使行后面出现了分号，令牌也会使该行的其余部分被忽略。 这不同于 [_ *$ $ (注释说明符)* *](-----comment-specifier-.md)，这会创建一个可由分号终止的注释。

例如，以下命令将显示 **eax** 和 **ebx**，但不显示 **ecx**：

```console
0:000> r eax; $$ some text; r ebx; * more text; r ecx
```

*\** 不会以任何方式处理由 * _ 或 [_ *$$* *](-----comment-specifier-.md)标记前缀的文本。 如果要执行远程调试，则在调试服务器中输入的注释将在调试客户端中不可见，反之亦然。 如果希望使注释文本在调试器中出现命令窗口以对所有参与方可见的方式显示，则应使用 [**echo (Echo 注释)**](-echo--echo-comment-.md)。
