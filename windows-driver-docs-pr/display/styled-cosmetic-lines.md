---
title: 带样式的装饰线条
description: 带样式的装饰线条
ms.assetid: 07e72190-7c8e-471e-9851-ccc037312c5c
keywords:
- 行 WDK GDI 样式外观
- 设置修饰 GDI WDK Windows 2000 显示，线条的样式
- 显示的图形驱动程序 WDK Windows 2000，样式修饰的行
- 绘制 WDK GDI，线条样式外观
- 带样式的外观行 WDK GDI
- WDK GDI 修饰线样式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff6006683ce59cfb0f38598a6fe3f0d9984fd20b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375991"
---
# <a name="styled-cosmetic-lines"></a>带样式的装饰线条


## <span id="ddk_styled_cosmetic_lines_gg"></span><span id="DDK_STYLED_COSMETIC_LINES_GG"></span>


[ **DrvStrokePath** ](https://msdn.microsoft.com/library/windows/hardware/ff556316)函数必须支持同时使用纯色画笔的任意剪辑其修饰的行的绘图。 该驱动程序可以对服务进行调用 GDI [ **PATHOBJ\_vEnumStartClipLines** ](https://msdn.microsoft.com/library/windows/hardware/ff568857)来预先计算剪辑。

修饰的样式是行的类似于几何加宽线，因为指定的重复的数组。 对于带样式的外观行中，数组项都是包含样式的步骤中的长度的长值。 由定义样式的步骤和像素之间的关系**xStyleStep**， **yStyleStep**，并**denStyleStep**中的字段[ **GDIINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff566484)由返回结构[ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211)函数。

当驱动程序调用[ **PATHOBJ\_bEnumClipLines**](https://msdn.microsoft.com/library/windows/hardware/ff568852)，以处理样式通过复杂剪辑修饰的行，GDI 修改的值[ **CLIPLINE** ](https://msdn.microsoft.com/library/windows/hardware/ff539416)结构的**iStyleState**成员来表示样式状态。 样式状态是返回到线段; 的第一个像素的偏移量也就是说，如果行不是经过剪切的呈现的第一个像素。 样式状态包含打包到 ULONG 值的两个 16 位值。 如果上限和下限是高序位，低序位 16 位样式状态的样式状态，称为样式位置的小数部分版本可计算为：

`
    style position = HIGH + LOW/denStyleStep
`

例如，如果中的值**iStyleState**为 1 和 2，并**denStyleStep**为 3，则为 5/3，样式的位置。 若要确定确切的绘制样式的开始位置样式数组中，执行该产品：

`
    style position * denStyleStep
`

在此示例中，使用**denStyleStep**值为 3，绘制的位置计算中排除的前五个 (5/3 \* 3) 样式数组的像素为单位。 也就是说，在此裁剪后的行的样式数组中的第六个像素开始绘制。

存在的 y 样式修饰的行和 x 样式修饰的行。 如果行扩展 dx 设备在 y 方向的 x 方向和 dy 单位中的单元，在行的 y-样式时满足以下条件：

`
    (dy * yStyleStep)  >=  (dx * xStyleStep)
`

在这种情况下，样式位置高级通过**yStyleStep**/**denStyleStep**每个像素高级沿 y 方向。

相反，行是 x 样式和通过高级样式位置**xStyleStep**/**denStyleStep**为满足以下条件时，在 x 方向的高级每个像素：

`
    (dx * xStyleStep)  >  (dy * yStyleStep)
`

当样式位置转到新的整数时，样式步骤向前移动在样式数组中的一个单元。

下图显示了多个外观的样式的行具有不同的周围。

![说明样式修饰的行的关系图](images/102-02.png)

在此图中，像素网格所示不是方形，但显示为它将用于 EGA 显示沿 x 方向的四个以像素为单位表示的沿 y 方向的三个像素的距离相同。 样式中的步骤[ **GDIINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff566484)结构确保带样式的行显示在其像素不是方形的显示器上任何斜率相同。 在此图中，样式数组 (由**pstyle**的成员[ **LINEATTRS** ](https://msdn.microsoft.com/library/windows/hardware/ff568195)结构) 是{1,1}，这是中断的行具有同等大小点和缺口。 驱动程序的值**xStyleStep**为 3， **yStyleStep** 4，并且**denStyleStep**为 12。

若要进一步说明，假设点阵打印机具有 144 dpi 水平分辨率和 72 dpi 垂直分辨率。 此外，假设最小点的点长度为 1/24 英寸。 若要支持此打印机，选择的最小的数字**xStyleStep**并**yStyleStep**的可补偿的打印机的纵横比，如 1 代表**xStyleStep**和2 (144/72) 用于**yStyleStep**，和 6 (144/24) 的**denStyleStep**。

如果 LA\_中的标志中设置备用位[ **LINEATTRS** ](https://msdn.microsoft.com/library/windows/hardware/ff568195)结构，特殊样式用于修饰的行。 在这种情况下，每个其他像素都是，而不考虑方向或纵横比。 样式数组时，都返回样式状态{1,1}并**xStyleStep**， **yStyleStep**，并且**denStyleStep**所有的一个。 换而言之，如果**lStyleState**为零，第一个像素都是上; 如果**lStyleState**为 1，第一个像素处于关闭状态。

如果 LA\_LINEATTRS 标志中设置 STARTGAP 位、 反转样式数组中元素的有意义。 第一个数组项指定的第一个间隙的长度，第二个条目指定长度的第一个破折号，等等。

 

 





