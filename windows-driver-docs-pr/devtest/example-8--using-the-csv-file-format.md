---
title: 示例 8 使用 CSV 文件格式
description: 示例 8 使用 CSV 文件格式
ms.assetid: 225365dd-57f8-4d35-a859-b881a104201f
keywords:
- Tracefmt WDK，CSV 格式
- CSV 格式 WDK Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19956cee86badc030dc3ca75ec866041f2142929
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378829"
---
# <a name="example-8-using-the-csv-file-format"></a>示例 8：使用 CSV 文件格式


以下命令将定向 Tracefmt 格式化跟踪消息输出文件 (**-o**) 作为以逗号分隔、 可变长度 (CSV) 格式文件：

```
tracefmt mytrace.etl -p c:\tracing -o mytrace.csv -csv -csvheader
```

此命令设置 mytrace.etl 跟踪日志文件中的跟踪消息。 它使用 **-p**参数来指定 TMF 文件的位置。

该命令使用 **-o**参数指定的名称和输出文件的位置，并使用.csv 文件扩展名的文件。 它使用**csv**参数来指定 CSV 格式，并 **-csvheader**参数将列标题的行添加到该文件。 默认情况下，该文件具有任何列标题。

在响应中，Tracefmt 前缀和消息字段之间使用逗号分隔格式的跟踪消息，并将其保存在 mytrace.csv 文件中。

 

 





