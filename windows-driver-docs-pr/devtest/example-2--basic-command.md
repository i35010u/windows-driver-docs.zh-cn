---
title: 示例 2 基本命令
description: 示例 2 基本命令
ms.assetid: 5e66b7f4-5cf6-4bfc-b432-d531ac6ac53c
keywords:
- Tracefmt WDK 命令
- WDK Tracefmt 命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb32465f493a45e20441ac9a0651e9724a7e0864
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344703"
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

此命令使用 EtlFile 参数来指定跟踪日志文件，mytrace.etl。 它使用 **-p**参数来指示存储 TMF 文件的目录并 **-o**参数来指定输出文件的备用名称。

在响应中，Tracefmt mytrace.etl 跟踪日志文件中的跟踪消息格式使用 TMF 文件 c： 驱动器中的\\跟踪目录。 它会创建一个名为 mytrace.txt 和名为 mytrace.txt.sum 的摘要文件的输出文件。
