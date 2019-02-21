---
title: 文本日志部分页脚的格式
description: 文本日志部分页脚的格式
ms.assetid: 3b804934-a695-4091-a3ef-03f7598cbe63
keywords:
- 部分页脚 WDK SetupAPI
- 格式 WDK SetupAPI 日志记录
- 文本日志 WDK SetupAPI，部分页脚
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4268b3ca86fd006cdcf448837d5bacf43b8f7d9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547695"
---
# <a name="format-of-a-text-log-section-footer"></a>文本日志部分页脚的格式


一个*文本日志部分页脚*关闭文本日志部分。 部分页脚包含两个条目。 部分页脚的第一个条目的格式包括"&lt; &lt; &lt; "前缀后, 跟*time_stamp*字段和字符串"部分中 end"。

```cpp
<<<  [time_stamp Section end]
```

格式*time_stamp*字段是与中所述的相同[文本日志部分标头的格式](format-of-a-text-log-section-header.md)。

第二个条目的格式包括"&lt; &lt; &lt; "前缀后, 跟字符串"Exit"和一个*状态*字段。 在以下示例中，斜体样式中的文本是部分创建者提供的特定部分的文本的占位符和粗体的字体样式的文本提供的 SetupAPI 日志记录：

```cpp
<<<  [Exit Status(status)]
```

状态字段的格式为"0x*hhhhhhhh*"，其中*hhhhhhhh*是 8 位十六进制数字。

如果状态字段不存在，在第一行的格式如下所示：

```cpp
<<<  [Exit]
```

以下是一种指定的退出状态为"0x00000000"并包含部分页脚*time_stamp*字段。

```cpp
<<<  [2005/02/13 22:06:28.109: Section end]
<<<  [Exit Status(0x00000000)]
```

 

 





