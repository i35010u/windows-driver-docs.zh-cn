---
title: 命令字符串格式
description: 命令字符串格式
keywords:
- 打印机命令 WDK Unidrv，字符串
- 命令字符串 WDK Unidrv
- 字符串 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d978b4b9ebc8c69e5baa4166d74fa12bd3443ba8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797639"
---
# <a name="command-string-format"></a>命令字符串格式





命令字符串用于指定 Unidrv 必须发送到打印机硬件的转义序列。 命令字符串可由以下元素组成：

-   带引号的文本字符串，格式如下：

    "*TextString*"

-   命令参数，格式如下：

    %*ArgumentType*{*StandardVariableExpression*}

Unidrv 支持在命令字符串中使用最多14个带引号的文本字符串和命令参数。

例如，可以按如下所示指定打印机的命令来设置矩形的灰色填充百分比：

```cpp
*Command: CmdRectGrayFill: "<1B>*c" %d{GrayPercentage} "g2P"
```

若要将百分号 (**%**) 发送到打印机，请在命令字符串中包含两个百分号字符 (**%%**) 。 如果百分比符号位于命令字符串的末尾，则必须使用十六进制等效项，如下所示：

**"**<em>字符串</em> **&lt; 25 25 &gt; "**。

 

 




