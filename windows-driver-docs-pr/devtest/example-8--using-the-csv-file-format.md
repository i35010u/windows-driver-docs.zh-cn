---
title: 使用 CSV 文件格式的示例8
description: 使用 CSV 文件格式的示例8
keywords:
- Tracefmt WDK，CSV 格式
- CSV 格式 WDK Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b0c1d70770a53db6833058857cee5efe3fd1ebd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804273"
---
# <a name="example-8-using-the-csv-file-format"></a>示例 8：使用 CSV 文件格式


以下命令指示 Tracefmt 将跟踪消息输出文件 (**-o**) 格式设置为逗号分隔的、可变长度 (CSV) 格式文件：

```
tracefmt mytrace.etl -p c:\tracing -o mytrace.csv -csv -csvheader
```

此命令格式化 mytrace 跟踪日志文件中的跟踪消息。 它使用 **-p** 参数指定 TMF 文件的位置。

该命令使用 **-o** 参数指定输出文件的名称和位置，并对该文件使用 .csv 文件扩展名。 它使用 **-csv** 参数指定 csv 格式，并使用 **-csvheader** 参数向该文件添加列标题行。 默认情况下，该文件没有列标头。

作为响应，Tracefmt 通过在前缀和消息字段之间使用逗号来设置跟踪消息的格式，并将它们保存在 mytrace.csv 文件中。

 

 





