---
title: 示例 1 没有参数
description: 示例 1 没有参数
ms.assetid: 6c37367e-88d5-43a3-bb80-57d53bb17326
keywords:
- Tracefmt WDK 参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe44fed927a35e4400abcee9c9bcced777106e7d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543920"
---
# <a name="example-1-no-parameters"></a>示例 1：没有参数

Tracefmt 没有任何所需的参数。 因此，最简单的 Tracefmt 命令如下所示：

```
tracefmt
```

在响应中，Tracefmt 格式化跟踪消息中的默认 c:\\logfile.etl 文件使用 TMF 文件中 %跟踪指定的路径\_格式\_搜索\_PATH %环境变量。 它会创建一个名为 Fmtfile.txt 和本地目录中名为 Fmtfile.txt.sum 条摘要消息文件的输出文件。
