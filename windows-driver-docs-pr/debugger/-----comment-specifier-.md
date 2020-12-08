---
title: '$ $ (注释说明符) '
description: 如果在命令开头出现两个货币符号 ( $ $ ) ，则该行的其余部分将被视为注释，除非注释以分号结束。
keywords:
- '注释标记 ($ $) '
- $ $ (注释说明符) Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- $$ (Comment Specifier)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f8608ea4f1a27e04b0879c3cc717a51c88f0a427
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800231"
---
# <a name="-comment-specifier"></a>$ $ (注释说明符) 


如果在命令开头出现两个货币符号 ( **$$** ) ，则该行的其余部分将被视为注释，除非注释以分号结束。


   $ $ [任意文本]


<a name="remarks"></a>备注
-------

**$$** 令牌的分析方式与任何其他调试器命令类似。 因此，如果要在另一个命令后创建注释，则必须在令牌前面加上 **$$** 一个分号。

**$$** 标记将导致文本被忽略，直到到达行尾或到达分号。 分号终止注释;分号后的文本将被分析为标准命令。 这不同于 * *\** _ [ (注释行说明符)](----comment-line-specifier-.md) 这样，即使存在分号，也会使该行的其余部分成为注释。

例如，以下命令将显示 _ *eax** 和 **ebx**，但不显示 **ecx**：

```console
0:000> r eax; $$ some text; r ebx; * more text; r ecx 
```

不会以任何方式处理以 **\* *_ 或 _* $$** 标记为前缀的文本。 如果要执行远程调试，则在调试服务器中输入的注释将在调试客户端中不可见，反之亦然。 如果希望使注释文本在调试器中出现命令窗口以对所有参与方可见的方式显示，则应使用 [**echo (Echo 注释)**](-echo--echo-comment-.md)。
