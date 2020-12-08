---
title: 续行符
description: 续行符
keywords:
- GPD 文件条目 WDK Unidrv，行继续
- 行延续 WDK GPD 文件
- 续行 WDK GPD 文件
- 继续符 WDK GPD 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36590d9c609c17710970f92155227f80dd332e34
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807945"
---
# <a name="line-continuation"></a>续行符





对于太长而无法放入单个行的[GPD 文件项](gpd-file-entries.md)，可以继续在后续行上。 若要继续某个条目，则第一个条目的前面必须加上一个加号 (+) 。 加号必须是行中的第一个字符，而不是前面的空格，如下面的示例中所示：

```cpp
*DeviceFonts:
+    LIST(
+        =RC_FONT_Courier_10pt_regular,
+        =RC_FONT_CGTimes_regular,
+        =RC_FONT_Univers_regular,
+        =RC_FONT_Univers_condensed_regular,
+        =RC_FONT_Antique_Olive_regular,
+        =RC_FONT_Albertus_Medium,
+        =RC_FONT_Albertus_Extra_Bold,
+        =RC_FONT_Courier_regular,
+        =RC_FONT_Letter_Gothic_regular,
+        =RC_FONT_Wingdings)
```

不需要在以下行的开头使用行继续符：

-   以星号开头的行。

-   以左大括号开头的行。

 

 




