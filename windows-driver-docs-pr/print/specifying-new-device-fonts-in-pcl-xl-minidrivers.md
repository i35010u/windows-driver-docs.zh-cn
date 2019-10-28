---
title: 在 PCL XL 微型驱动程序中指定新的设备字体
description: 在 PCL XL 微型驱动程序中指定新的设备字体
ms.assetid: 395b9200-4514-4b05-b417-15d4896914f4
keywords:
- PCL XL 矢量图形 WDK Unidrv，设备字体
- 设备字体 WDK PCL XL
- 字体 WDK PCL XL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3def1c88b16dba522897be9525c6b0b169cfbbc5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840405"
---
# <a name="specifying-new-device-fonts-in-pcl-xl-minidrivers"></a>在 PCL XL 微型驱动程序中指定新的设备字体





如果要支持 PCL XL 微型驱动程序中的新设备字体，则必须为这些设备字体创建*Unidrv 字体指标（UFM）* 文件。

UFM 文件采用以下格式：

[**UNIFM\_HDR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_unifm_hdr)结构，用作 UFM 文件的标头

[**UNIDRVINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_unidrvinfo)结构

[**IFIMETRICS**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_ifimetrics)结构

[**EXTTEXTMETRIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_exttextmetric)结构

字符宽度表

必须将格式正确的字体选择命令放在 UFM 文件中的正确位置。 字体选择命令由16个字节组成：选择字体、为空格字符提供一个字节，以及容纳符号集编号的数字所需的字节数。

下面是一个示例，演示字体选择命令在 UFM 文件中的显示方式。 （第二行中的数字显示 "字体选择" 命令中每个字符的位置。）

```cpp
CG Omega    BdIt 629
12345678901234567890
```

"字体名称" 和 "样式"，CG Omega BdIt （粗体/斜体）占用前16个字节。 在此之后，有一个空格字符，该字符将字体名称与符号集编号隔开。 符号集编号629将占用最后三个字节。 Unidrv 分析 UFM 文件中的字体选择命令，并分别发送字体选择命令和符号集编号。

上一示例中讨论的字体名称和符号集编号是**SetFont**运算符所需的三个属性中的两个，它们将出现在驱动程序的输出数据中。 在下面的示例中，此运算符的**FontName**和**SymbolSet**属性设置为与前面的示例中相同的值。 第三个属性**CharSize**设置为值100。

```cpp
ubyte_array (CG Omega    BdIt) FontName
real32 100 CharSize
uint16 629 SymbolSet
SetFont
```

有关**SetFont**字体选择命令的详细信息，请参阅*PCL XL 功能参考协议类 2.0*文档。 （此资源可能在某些语言和国家/地区不可用。）

 

 




