---
title: 设置排除列表
description: 设置排除列表
keywords:
- SymProxy，排除列表
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48a57e9a2c24ba1b30b8fe8d5b1660de136b8ce1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818631"
---
# <a name="setting-up-exclusion-lists"></a>设置排除列表


在某些环境中，你可能会发现自己调试的系统中加载了大量模块，但无法获取符号。 如果有第三方供应商调用的代码，则通常会出现这种情况。 这可能会导致多次尝试查找符号，这是一项耗时且 clogs 的网络资源。 若要缓解这种情况，可以使用 *排除列表* 来指定应从搜索中排除的符号。 此功能存在于客户端调试器中，但你也可以将 SymProxy 筛选器配置为使用其自己的排除列表，并防止此类网络活动最可能占用资源。

排除列表由要阻止处理的文件的名称组成。 文件名可以包含通配符。 例如：

```console
dbghelp.pdb
symsrv.*
mso*
```

可以通过两种方式实现此列表。 第一个文件位于 .ini 文件% WINDIR% \\ system32 \\ inetsrv \\Symsrv.ini 中。 名为 "排除" 的部分应包含以下列表：

```console
[exclusions]
dbghelp.pdb
symsrv.*
mso*
```

或者，你可以将排除项存储在注册表中。 创建名为

```text
HKLM\Software\Microsoft\Symbol Server\Exclusions
```

在此注册表项中，将 "文件名" 列表以字符串值的形式存储 (REG \_ SZ) 。 字符串值的名称将用作要排除的文件名。 字符串值的内容可以作为注释来描述排除文件的原因。

SymProxy 每半小时从排除列表读取一次，以便你无需重新启动 Web 服务即可看到更改生效。 将文件添加到注册表或 .ini 文件中的列表，并等待一小段时间，以便使用排除项。

**注意**   SymProxy 不支持同时使用 Symsrv.ini 和注册表。 如果 .ini 文件存在，则使用该文件。 否则，将检查注册表。

 

 

 





