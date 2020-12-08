---
title: 示例1无参数
description: 示例1无参数
keywords:
- Tracefmt WDK，参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef5e6b4aca81c0b5482cc13c415316a7a732ff70
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787641"
---
# <a name="example-1-no-parameters"></a>示例 1：无参数

Tracefmt 没有必需的参数。 因此，最简单的 Tracefmt 命令如下所示：

```
tracefmt
```

在响应中，Tracefmt \\ 通过使用由% trace \_ FORMAT \_ SEARCH \_ path% 环境变量指定的路径中的 TMF 文件，在默认 C： logfile 文件中设置跟踪消息的格式。 它在本地目录中创建名为 Fmtfile.txt 的输出文件和名为 Fmtfile.txt 的摘要消息文件。
