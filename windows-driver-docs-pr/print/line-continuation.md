---
title: 续行符
description: 续行符
ms.assetid: ee4dbb3d-ba9d-45bb-82dd-ecee4682ae63
keywords:
- GPD 文件条目 WDK Unidrv，行继续符
- 行继续符 WDK GPD 文件
- 连续的行 WDK GPD 文件
- 继续符 WDK GPD 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: facfa623fa383c257d7e505e4df6c97975ace68e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562337"
---
# <a name="line-continuation"></a>续行符





[GPD 文件条目](gpd-file-entries.md)是太长而无法容纳到一个单一行可以继续后续行上。 若要继续一个条目，第一个之后的每一行必须加一个加号 （+）。 正号必须在行中，而无需上述的空白区域的第一个字符，如下面的示例中所示：

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

不需要使用以下行开头的行继续符：

-   以星号开头的行。

-   左大括号开始的行。

 

 




