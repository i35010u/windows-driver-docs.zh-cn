---
title: 硬件中的字体
description: 硬件中的字体
keywords:
- 打印机字体说明 WDK Unidrv，硬件驻留字体
- 硬件驻留字体 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1ed409ccf568b4b40bed7a5ec01121f95c5b153
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835831"
---
# <a name="hardware-resident-fonts"></a>硬件中的字体





如果你的打印机包含硬件驻留字体，则必须在 ufm 或 ifi 文件中提供这些字体的字体规格规范。

每个硬件驻留字体都在单独的 ufm 或 ifi 文件中进行了介绍。 若要使这些文件可供 Unidrv 使用，请执行以下操作：

-   在打印机的资源 DLL 中，通过使用 RC ufm 资源类型来指定 ufm 文件 \_ ，并使用 rc \_ 字体资源类型指定 ifi 文件。

-   在打印机的 GPD 文件中，使用 \* ResourceDLL 属性指定资源 DLL 的名称。

-   在打印机的 GPD 文件中，使用 \* DeviceFonts 条目来指定与 \_ 资源 DLL 中 rc UFM 或 rc 字体条目关联的资源标识符 \_ 。

DeviceFonts 条目的格式 \* 如下所示：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>* DeviceFonts： LIST (</strong> <em>FontResourceID</em><strong>，</strong> <em>FontResourceID</em><strong>，</strong> .。。<strong>) </strong></p></td>
</tr>
</tbody>
</table>

 

其中， *FontResourceID* 是 \_ 与 UFM 文件关联的 rc UFM 资源标识符，或 \_ 与 IFI 文件关联的 rc 字体资源标识符。

下面是一个示例：

```cpp
*% Assume that RC_FONT_xxx ids are references to 
*% value macros defined by the GPD file creator.
*DeviceFonts: LIST(=RC_FONT_COURIER10, =RC_FONT_ARIALR,
+                  =RC_FONT_ARIALI, =RC_FONT_ARIALB, 
+                  =RC_FONT_ARIALBI, =RC_FONT_TIMESNRR,
+                  =RC_FONT_TIMESNRI, =RC_FONT_TIMESNRB,
+                  =RC_FONT_TIMESNRBI)
```

可以 \* 在 [Unidrv 微型驱动程序](unidrv-minidrivers.md)中包含多个 DeviceFonts 条目。 GPD 分析器将多个条目连接起来，并使所有列出的字体可用于打印机功能的所有配置。 如果需要指定某些字体仅适用于某些配置，则可以 \* 在 [条件语句](conditional-statements.md)中包含 DeviceFonts 项。

 

 




