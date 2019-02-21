---
title: 命令字符串格式
description: 命令字符串格式
ms.assetid: 3b33b261-08c7-4441-94f5-6c9de53ae349
keywords:
- 打印机命令 WDK Unidrv，字符串
- 命令字符串 WDK Unidrv
- 字符串 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f34b2a6588ce5d66f3557a0eed5a483fabf1954
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547750"
---
# <a name="command-string-format"></a>命令字符串格式





命令字符串用于指定 Unidrv 必须将发送到打印机硬件的转义序列。 命令字符串可以组成以下元素：

-   带引号的文本字符串，具有以下格式：

    "*TextString*"

-   命令参数，具有以下格式：

    %*ArgumentType*{*StandardVariableExpression*}

Unidrv 命令字符串中支持最多 14 带引号的文本字符串和命令参数。

例如，可能按如下所示指定打印机的命令以设置矩形的灰色填充百分比：

```cpp
*Command: CmdRectGrayFill: "<1B>*c" %d{GrayPercentage} "g2P"
```

若要发送百分号 (**%**) 到打印机，包括 %2%的符号字符 (**%%**) 中的命令字符串。 如果百分比符号位于命令字符串的末尾，则必须使用十六进制等效值，如：

**"**<em>字符串</em>  **&lt;25 25&gt;"**。

 

 




