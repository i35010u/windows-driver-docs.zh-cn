---
title: 示例2基本命令
description: 示例2基本命令
keywords:
- Tracefmt WDK，命令
- 命令 WDK Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 666ea719f9a07bf7d33b89c435bd33a666d16bf5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839147"
---
# <a name="example-2-basic-command"></a>示例 2：基本命令

用于启动 Tracefmt 的基本命令的语法如下所示：

```
tracefmt EtlFile -p TMFPath -o OutputFile
```

例如，

```
tracefmt mytrace.etl -p c:\tracing -o mytrace.txt
```

此命令使用 EtlFile 参数来指定跟踪日志文件 mytrace。 它使用 **-p** 参数来指示存储 TMF 文件的目录，并使用 **-o** 参数指定输出文件的备用名称。

作为响应，Tracefmt 使用 c： trace 目录中的 TMF 文件设置 mytrace 跟踪日志文件中跟踪消息的格式 \\ 。 它会创建一个名为 mytrace.txt 的输出文件和一个名为 mytrace.txt 的摘要文件。
