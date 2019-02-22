---
title: 设置排除列表
description: 设置排除列表
ms.assetid: 0b50e8a6-f68c-43e5-b8d5-4b2c40252d38
keywords:
- SymProxy，排除列表
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59e2ed0d6c3b2e7cd06779dc7cabae84c310cf9d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541841"
---
# <a name="setting-up-exclusion-lists"></a>设置排除列表


在某些环境中，您可能发现自己调试具有大量加载的模块不能为其获取符号的系统。 这通常是这种情况，如果您的代码调用的第三方供应商。 这可能导致很多的失败尝试查找符号，这很耗时并且会阻塞网络资源。 若要缓解这种情况下，可以使用*排除列表*以指定应从搜索中排除的符号。 此功能存在于客户端调试器，但还可以配置要使用其自己的 SymProxy 筛选器排除列表，并防止此类是最有可能会占用资源的网络活动。

排除列表由你想要防止处理的文件的名称组成。 文件名称可以包含通配符。 例如：

```console
dbghelp.pdb
symsrv.*
mso*
```

可以通过两种方式实现列表。 第一种是在.ini 文件中，%WINDIR%\\system32\\inetsrv\\Symsrv.ini。 一个名为"排除"部分应包含列表：

```console
[exclusions]
dbghelp.pdb
symsrv.*
mso*
```

或者，也可以在注册表中存储生成的排除项。 创建名为

```text
HKLM\ Software\Microsoft\Symbol Server\Exclusions
```

将文件名称列表存储为字符串值 (REG\_SZ) 该注册表项中。 字符串值的名称将用作要排除的文件名称。 字符串值的内容可以用作注释，说明为什么该文件已被排除。

SymProxy 读取从排除列表中每半小时，以便不需要重新启动 Web 服务以查看更改生效。 将文件添加到注册表或.ini 文件中的列表，并等到生成的排除项，用于在短时间。

**请注意**   SymProxy 不支持使用 Symsrv.ini 和注册表。 如果.ini 文件存在，则使用它。 否则，检查注册表。

 

 

 





