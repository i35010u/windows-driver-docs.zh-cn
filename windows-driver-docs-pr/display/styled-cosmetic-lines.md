---
title: 带样式的装饰线条
description: 带样式的装饰线条
ms.assetid: 07e72190-7c8e-471e-9851-ccc037312c5c
keywords:
- 线条 WDK GDI，样式修饰
- GDI WDK Windows 2000 显示，线条，样式修饰
- 图形驱动程序 WDK Windows 2000 显示，线条，样式修饰
- 绘制 WDK GDI，线条，样式修饰
- 样式修饰线 WDK GDI
- 修饰线 WDK GDI，样式化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f59c27443b2578ba30c1c4d50b1716c36a0ed9d
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714750"
---
# <a name="styled-cosmetic-lines"></a>带样式的装饰线条


## <span id="ddk_styled_cosmetic_lines_gg"></span><span id="DDK_STYLED_COSMETIC_LINES_GG"></span>


[**DrvStrokePath**](/windows/win32/api/winddi/nf-winddi-drvstrokepath)函数必须支持使用纯色画笔的任意剪辑绘制修饰线条。 驱动程序可以调用 GDI 服务 [**PATHOBJ \_ vEnumStartClipLines**](/windows/win32/api/winddi/nf-winddi-pathobj_venumstartcliplines) 来预计算剪辑。

修饰线的样式类似于几何宽线的样式，因为它是由重复数组指定的。 对于样式的修饰线，数组项是包含样式步骤中的长度的长值。 样式步骤和像素之间的关系由[**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev)函数返回的[**GDIINFO**](/windows/win32/api/winddi/ns-winddi-_gdiinfo)结构中的**xStyleStep**、 **yStyleStep**和**denStyleStep**字段定义。

当驱动程序调用 [**PATHOBJ \_ bEnumClipLines**](/windows/win32/api/winddi/nf-winddi-pathobj_benumcliplines)来处理复杂剪辑中的样式修饰线时，GDI 将修改 [**CLIPLINE**](/windows/win32/api/winddi/ns-winddi-_clipline) 结构的 **iStyleState** 成员的值以表示样式状态。 样式状态是返回到直线段第一个像素的偏移量;也就是说，如果未剪裁线条，将呈现第一个像素。 样式状态包括打包到 ULONG 值中的 2 16 位值。 如果 "高" 和 "低" 是样式状态的高阶和低序位16位，则样式状态的小数版本（称为样式位置）可按以下方式计算：

`
    style position = HIGH + LOW/denStyleStep
`

例如，如果 **iStyleState** 中的值为1和2，并且 **denStyleStep** 为3，则 style 位置为5/3。 若要确定样式绘制在样式数组中的起始位置，请采用以下产品：

`
    style position * denStyleStep
`

在此示例中，如果 **denStyleStep** 值为3，则计算绘图位置以排除样式数组的前5个 (5/3 \* 3) 像素。 也就是说，从此剪裁线条样式数组的第六个像素开始绘制。

有 y 样式的修饰线和 x 样式的修饰线条。 如果某行在 y 方向上沿 x 方向和 dy 个单位扩展 dx 设备单位，则在满足以下条件时，将行设置为 y 样式：

`
    (dy * yStyleStep)  >=  (dx * xStyleStep)
`

在这种情况下，样式位置将由**yStyleStep** / **denStyleStep**为 y 方向的每个像素的高级。

相反，线条是 x 样式的，如果满足以下条件，则每个像素的**xStyleStep** / **denStyleStep**的样式位置都是高级的：

`
    (dx * xStyleStep)  >  (dy * yStyleStep)
`

当样式位置前进到新的整数时，样式步骤会在样式数组中前进一个单元。

下图显示了多个具有不同倾斜的修饰样式线条。

![说明样式修饰线条的关系图](images/102-02.png)

在此图中，所显示的像素网格不是正方形的，而是显示为对于 EGA 显示，其中 x 方向的四个像素表示与 y 方向上的三个像素相同的距离。 [**GDIINFO**](/windows/win32/api/winddi/ns-winddi-_gdiinfo)结构中的样式步骤确保样式的线条在其像素不是正方形的任何斜度上显示为相同。 在此图中，样式数组 (由[**LINEATTRS**](/windows/win32/api/winddi/ns-winddi-_lineattrs)结构的**pstyle**成员定义) 是 {1,1} ，这是一个具有相同大小的点和间隙的破断线。 驱动程序的 **xStyleStep** 值为3， **yStyleStep** 为4， **denStyleStep** 为12。

为了进一步说明，假设点阵打印机的水平分辨率为 144 dpi，分辨率为 72 dpi。 此外，假设最小点的点长为 1/24 英寸。 若要支持此打印机，请选择 **xStyleStep** 和 **yStyleStep** 的最小数目，该数字可补偿打印机的纵横比，例如，1表示 **xStyleStep** ，2 (144/72) 用于 **YStyleStep**，6 (144/24) 用于 **denStyleStep**。

如果在 \_ [**LINEATTRS**](/windows/win32/api/winddi/ns-winddi-_lineattrs) 结构中的标志处设置了 LA 备用位，则将使用一种特殊的样式作为修饰线。 在这种情况下，无论方向或纵横比如何，每隔一个像素都是打开的。 如果样式数组为 {1,1} ，且 **xStyleStep**、 **yStyleStep**和 **denStyleStep** 均为1，则返回样式状态。 换言之，如果 **lStyleState** 为零，则第一个像素为 on;如果 **lStyleState** 为 one，则第一个像素为 off。

如果 \_ 在 LINEATTRS 标志中设置了 LA STARTGAP 位，则将反转样式数组中元素的含义。 第一个数组条目指定第一个间隙的长度，第二个条目指定第一个短划线的长度，依此类推。

 

