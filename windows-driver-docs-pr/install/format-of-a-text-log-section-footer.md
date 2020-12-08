---
title: 文本日志部分页脚的格式
description: 文本日志部分页脚的格式
keywords:
- 节页脚 WDK Setupapi.log
- 格式化 WDK Setupapi.log 日志记录
- 文本日志 WDK Setupapi.log，节页脚
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d96009ec9463b874a2b2ab415f2ad63c772db7b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820183"
---
# <a name="format-of-a-text-log-section-footer"></a>文本日志部分页脚的格式


*文本日志节页脚* 将关闭文本日志节。 节页脚包含两个条目。 节页脚第一项的格式包括 " &lt; &lt; &lt; " 前缀，后跟一个 *time_stamp* 字段和字符串 "section end"。

```cpp
<<<  [time_stamp Section end]
```

*Time_stamp* 字段的格式与 [文本日志节标头格式](format-of-a-text-log-section-header.md)中所述的格式相同。

第二个条目的格式包括 " &lt; &lt; &lt; " 前缀，后跟字符串 "Exit" 和 *status* 字段。 在下面的示例中，以斜体字体样式显示的文本是部分特定文本的占位符，该文本由部分创建者提供，粗体字体样式的文本由 Setupapi.log 日志记录提供：

```cpp
<<<  [Exit Status(status)]
```

状态字段的格式为 "0x *hhhhhhhh*"，其中 *hhhhhhhh* 为8位十六进制数字。

如果 "状态" 字段不存在，则第一行的格式如下所示：

```cpp
<<<  [Exit]
```

下面是指定退出状态 "0x00000000" 并包括 *time_stamp* 字段的节页脚示例。

```cpp
<<<  [2005/02/13 22:06:28.109: Section end]
<<<  [Exit Status(0x00000000)]
```

 

 





