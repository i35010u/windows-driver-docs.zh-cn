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
ms.openlocfilehash: 90596e8d09a7a10edb939e19cf1063a392e81bc3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561985"
---
# <a name="specifying-new-device-fonts-in-pcl-xl-minidrivers"></a>在 PCL XL 微型驱动程序中指定新的设备字体





如果你想要在 PCL XL 微型驱动程序中支持新的设备字体，则必须创建*Unidrv 字体规格 (UFM)* 这些设备字体的文件。

UFM 文件采用以下格式：

一个[ **UNIFM\_HDR** ](https://msdn.microsoft.com/library/windows/hardware/ff563587)结构，它可用作 UFM 文件的标头

一个[ **UNIDRVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff562872)结构

[ **IFIMETRICS** ](https://msdn.microsoft.com/library/windows/hardware/ff567418)结构

[ **EXTTEXTMETRIC** ](https://msdn.microsoft.com/library/windows/hardware/ff548801)结构

字符宽度表

格式正确的字体选择命令必须位于 UFM 文件中的正确位置。 保存符号的数字所需的所有字节都集编号和字体选择命令包含的字体选择，空格字符，1 个字节的 16 个字节。

下面是举例说明如何在 UFM 文件中显示字体选择命令。 （第二行中的数字显示每个字符的位置中的字体选择命令。）

```cpp
CG Omega    BdIt 629
12345678901234567890
```

字体和样式，CG Omega BdIt （粗体/斜体） 会占用前 16 个字节。 之后，没有单个空格字符，哪些将从该符号的字体名称集编号。 符号设置数字，629，占用的最后三个字节。 Unidrv 分析 UFM 文件中的字体选择命令，并将字体选择命令发送和符号分别设置数量。

字体名称和设置数字的符号前面的示例中所述是所需的三个属性的两个**SetFont**运算符，从该驱动程序会显示在输出数据。 在以下示例中， **FontName**并**SymbolSet**此运算符的属性设置为相同的值，如前面的示例所示。 第三个属性， **CharSize**，设置为 100 的值。

```cpp
ubyte_array (CG Omega    BdIt) FontName
real32 100 CharSize
uint16 629 SymbolSet
SetFont
```

有关详细信息**SetFont**字体选择命令，请参阅*PCL XL 功能引用协议类 2.0*文档。 （此资源可能不会在某些语言和国家/地区中可用。）

 

 




