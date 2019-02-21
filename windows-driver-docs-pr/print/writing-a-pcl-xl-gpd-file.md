---
title: 写入 PCL XL GPD 文件
description: 写入 PCL XL GPD 文件
ms.assetid: 35abc33a-a046-452b-b650-5c4f626bf6cb
keywords:
- PCL XL 矢量图形 WDK Unidrv，写入 GPD 文件
- GPD 文件 WDK Unidrv PCL XL
- 排序 WDK PCL XL 命令
- 写入 PCL XL GPD 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b89db1789728e3d220193fd5247cdd6ceddd67a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519523"
---
# <a name="writing-a-pcl-xl-gpd-file"></a>写入 PCL XL GPD 文件





本部分提供有关编写 PCL XL GPD 文件的常规信息，如哪些文件 GPD 文件应包括，如何启用 PCL XL 在 GPD 文件中，以及如何进行排序的 PCL XL 流中的 PCL XL 命令。

Windows Driver Kit (WDK) 中包含示例 PCL XL GPD 文件 (p6sample.gpd) \\src\\打印\\微型\\mdw\\向量\\pcl6 目录。 （此资源可能不会在某些语言和国家/地区中可用。）

### <a name="files-to-include"></a>要包含的文件

若要编写基于 GPD 的微型驱动程序，使用预处理器指令\*包括以指定下列 GPD 文件：

pclxl.gpd-包含宏的 PCL XL 运算符，以便您可以编写更轻松地阅读和理解的 GPD 代码。 例如，你可以编写 =**BeginPage**而不是&lt;43&gt;。

p6disp.gpd-包含用于 pcl5eres.dll 和 pclxl.dll 中包含的资源字符串的宏。

p6font.gpd-包含用于字体 pclxl.dll 中包含的宏。

pjl.gpd-包含用于 PJL 命令的宏。

除了前面提到的文件，包括标准 GPD 文件、 stdnames.gpd 和 ttfsub.gpd。

下面的示例演示如何将这些文件包括 GPD 文件中。

```cpp
*Include: stdnames.gpd
*Include: ttfsub.gpd
*Include: pclxl.gpd
*Include: p6disp.gpd
*Include: p6font.gpd
*Include: pjl.gpd
```

### <a name="enabling-pcl-xl-support-in-the-gpd-file"></a>启用 GPD 文件中的 PCL XL 支持

若要启用 PCL XL 向量支持，只需设置\*个性属性。 这是通过以下方式：

```cpp
*Personality: = PERSONALITY_PCLXL
```

个性\_PCLXL 常量 stdnames.gpd 中定义。

示例 GPD 文件、 p6sample.gpd，包含在 WDK 帮助开发人员创建新的 PCL XL 微型驱动程序。

### <a name="pcl-xl-command-ordering"></a>PCL XL 命令排序

命令的顺序是在 PCL XL 比 PCL 5 中更为重要。 PCL 流中的小错误不是可能会影响在该作业，但 PCL XL 命令是仅在特定时间点在流中有效，因此 PCL XL (PCL 6) 中的任何错误将导致发出一个 XL 错误页面。 例如，不能发送 BeginPage 运算符具有发送 BeginSession 运算符之前。

PCL XL 流具有类似于以下形式。 （所示的缩进是仅用于强调成对出现这些运算符的点。）

```cpp
PJL commands
BeginSession
  OpenDataSource
    BeginPage
      <page data>
    EndPage
  CloseDataSource
EndSession
PJL commands
```

PCL XL 流是由前面和后面 PJL 命令。 将 PCL XL 流本身与 BeginSession 运算符，开头和结尾 EndSession 运算符。 在配对的运算符，还有另一对运算符：OpenDataSource 和 CloseDataSource。 在该运算符对来自一个或多个 BeginPage/EndPage 运算符对，有一对每个页面发送到打印机。 页数据，其中描述了单个页面的呈现方式，由 BeginPage/EndPage 运算符对括起来。

有关所有 PCL XL 运算符的详细信息，请参阅*PCL XL 功能引用协议类 2.0*文档。

### <a name="additional-information-about-pcl-xl-gpd-files"></a>有关 PCL XL GPD 文件的其他信息

在 PCL XL GPD 文件\*FontFormat 属性名称，可指定下载字体的方法，仅限于两个值：为 HPPCL\_轮廓，然后为 HPPCL\_RES。 第一个值表示 Unidrv 下载 TrueType 大纲数据。 第二个值表示 Unidrv 下载位图软字体数据。

限制要下载的字体的数量或限制要下载给定字体中的字符数，IHV 可以降低出现打印机内存使用情况。 \*MinFontID 和\*MaxFontID 属性名称用来通知 Unidrv 下载其 Id 位于指定这些值的范围内的软字体。 同样， \*MinGlyphID 和\*MaxGlyphID 属性名称被用来限制将下载到那些特定范围内的给定字体的标志符号的数量。

Unidrv 将在假定每个 GPD 文件都包含其自身抖动矩阵操作。 此外建议每个设备都有其自己的抖动矩阵。 中指定抖动矩阵\*功能：抖动[自定义的功能](customized-features.md)。

 

 




