---
title: 硬件中的字体
description: 硬件中的字体
ms.assetid: 359735c2-bfa3-4c32-82a5-1d455c4eacb1
keywords:
- 打印机字体说明 WDK Unidrv，驻留在硬件中的字体
- 驻留在硬件中的字体 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c43bb2017697472d74065064bb9e57fbc258063
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360533"
---
# <a name="hardware-resident-fonts"></a>硬件中的字体





如果您的打印机包含驻留在硬件中的字体，必须提供.ufm 或.ifi 文件内这些字体的字体标准规范。

单独.ufm 或.ifi 文件中描述的每个硬件常驻字体。 若要使这些文件可供 Unidrv，执行以下操作：

-   在打印机的资源 DLL 中，指定.ufm 文件使用 RC\_UFM 资源类型，并指定使用 RC.ifi 文件\_字体资源类型。

-   在打印机的 GPD 文件中，使用\*项 ResourceDLL 属性来指定资源 DLL 的名称。

-   在打印机的 GPD 文件中，使用\*DeviceFonts 项以指定与 RC 相关联的资源标识符\_UFM 或 RC\_字体资源 DLL 中的条目。

格式\*DeviceFonts 条目如下所示：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>* DeviceFonts:LIST (</strong><em>FontResourceID</em><strong>,</strong> <em>FontResourceID</em><strong>,</strong> ...<strong>)</strong></p></td>
</tr>
</tbody>
</table>

 

其中*FontResourceID*是 RC\_UFM 与.ufm 文件或 rc 版关联的资源标识符\_与.ifi 文件相关联的字体资源标识符。

以下是一个示例：

```cpp
*% Assume that RC_FONT_xxx ids are references to 
*% value macros defined by the GPD file creator.
*DeviceFonts: LIST(=RC_FONT_COURIER10, =RC_FONT_ARIALR,
+                  =RC_FONT_ARIALI, =RC_FONT_ARIALB, 
+                  =RC_FONT_ARIALBI, =RC_FONT_TIMESNRR,
+                  =RC_FONT_TIMESNRI, =RC_FONT_TIMESNRB,
+                  =RC_FONT_TIMESNRBI)
```

可以包含多个\*DeviceFonts 中的条目[Unidrv 微型驱动程序](unidrv-minidrivers.md)。 GPD 分析器串联多个条目，并使所有列出的字体可用于所有配置的打印机的功能。 如果你需要指定一些字体是仅适用于某些配置，可以包括\*内的 DeviceFonts 条目[条件语句](conditional-statements.md)。

 

 




