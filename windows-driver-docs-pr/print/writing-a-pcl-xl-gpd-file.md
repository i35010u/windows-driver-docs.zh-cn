---
title: 编写 PCL XL GPD 文件
description: 编写 PCL XL GPD 文件
keywords:
- PCL XL vector graphics WDK Unidrv，编写 GPD 文件
- GPD 文件 WDK Unidrv，PCL XL
- 命令顺序 WDK PCL XL
- 正在写入 PCL XL GPD 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbf48f1801240f6f410379ffc844993d83cdc4d7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831181"
---
# <a name="writing-a-pcl-xl-gpd-file"></a>编写 PCL XL GPD 文件





本部分提供有关编写 PCL XL GPD 文件的常规信息，例如 GPD 文件应包含的文件、如何在 GPD 文件中启用 PCL XL，以及如何在 PCL XL 流中对 PCL XL 命令进行排序。

Windows 驱动程序工具包 (WDK) 在 \\ src \\ 打印 \\ 迷你 \\ mdw \\ 矢量 \\ PCL6 目录中包含一个示例 PCL XL GPD 文件 (p6sample) GPD。  (此资源可能在某些语言和国家/地区不可用。 ) 

### <a name="files-to-include"></a>要包括的文件

若要编写基于 GPD 的微型驱动程序，请使用预处理器指令 \* Include 来指定以下 GPD 文件：

pclxl. gpd--包含 PCL XL 运算符的宏，以便可以编写更易于阅读和理解的 GPD 代码。 例如，可以编写 =**BeginPage** 而不是 &lt; 43 &gt; 。

p6disp. gpd--包含 pcl5eres.dll 和 pclxl.dll 中包含的资源字符串的宏。

p6font. gpd--包含 pclxl.dll 中所包含字体的宏。

pjl. gpd--包含用于 PJL 命令的宏。

除了上述文件外，还包括标准 GPD 文件 stdnames. GPD 和 ttfsub。

下面的示例演示如何将这些文件包括在 GPD 文件中。

```cpp
*Include: stdnames.gpd
*Include: ttfsub.gpd
*Include: pclxl.gpd
*Include: p6disp.gpd
*Include: p6font.gpd
*Include: pjl.gpd
```

### <a name="enabling-pcl-xl-support-in-the-gpd-file"></a>在 GPD 文件中启用 PCL XL 支持

若要启用 PCL XL 矢量支持，只需设置 " \* 个性" 特性。 这可以通过以下方式完成：

```cpp
*Personality: = PERSONALITY_PCLXL
```

\_在 stdnames 中定义了个性 PCLXL 常量。

WDK 中包含一个示例 GPD 文件 p6sample GPD，可帮助开发人员创建新的 PCL XL 微型驱动程序。

### <a name="pcl-xl-command-ordering"></a>PCL XL 命令排序

与 PCL-5 相比，命令的顺序在 PCL XL 中更为重要。 PCL 流中的小错误不会影响作业，但 PCL XL 命令仅在流中的某些位置有效，因此 PCL XL (PCL-6) 会导致发出 XL 错误页。 例如，在发送 BeginSession 操作员之前，不能发送 BeginPage 操作员。

PCL XL stream 的格式如下所示。  (显示的缩进仅用于强调这些运算符成对出现的点 ) 

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

PCL XL stream 前面带有 PJL 命令。 PCL XL stream 本身以 BeginSession 运算符开头，以 EndSession 运算符结尾。 在该对运算符中，有另一对运算符： OpenDataSource 和 CloseDataSource。 在该运算符对中，每个发送到打印机的页面都有一个或多个 BeginPage/EndPage 运算符对。 页面数据（描述单个页面的呈现方式）由 BeginPage/EndPage 运算符对括起来。

有关所有 PCL XL 运算符的详细信息，请参阅 *PCL Xl 功能参考协议类 2.0* 文档。

### <a name="additional-information-about-pcl-xl-gpd-files"></a>有关 PCL XL GPD 文件的其他信息

在 PCL XL GPD 文件中， \* FontFormat 属性名称（指定下载字体的方式）限制为两个值： HPPCL \_ 轮廓和 HPPCL \_ RES。 第一个值指示 Unidrv 要下载 TrueType 大纲数据。 第二个值指示 Unidrv 要下载位图软字体数据。

IHV 可以通过限制要下载的字体数量或限制在给定字体中下载的字符数来减少打印机内存使用量。 \*MinFontID 和 \* MaxFontID 属性名称用于通知 Unidrv 下载其 id 位于这些值所指定范围内的软字体。 同样， \* MinGlyphID 和 \* MaxGlyphID 特性名称用于限制给定字体中要下载到特定范围内的字形的数量。

Unidrv 在假设每个 GPD 文件都包含其自己的抖动矩阵时进行操作。 还建议每个设备都有其自己的抖动矩阵。 仿色矩阵在功能中指定 \* ：仿色 [自定义功能](customized-features.md)。

 

 




