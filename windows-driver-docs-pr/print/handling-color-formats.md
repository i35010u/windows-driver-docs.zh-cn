---
title: 处理颜色格式
description: 处理颜色格式
ms.assetid: 4d0faba6-1994-474f-a5d3-e25cd2800cf7
keywords:
- Unidrv，颜色格式
- 颜色格式 WDK Unidrv
- ColorMode 功能
- 打印机颜色格式 WDK Unidrv
- 颜色管理 WDK 打印，格式
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3f7307002a4352f9711d3bda48bec0f9024fb69
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360571"
---
# <a name="handling-color-formats"></a>处理颜色格式





每个打印机支持的颜色格式指定为 ColorMode 功能的选项。 通过使用[选项为 ColorMode 功能特性](option-attributes-for-the-colormode-feature.md)，可以描述您的打印机接受每个颜色格式。 下表说明了 Unidrv 可以处理的颜色数据格式。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>颜色平面数</th>
<th>每像素位数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在设备 (<em>DevNumOfPlanes)</td>
<td>在设备 (</em>DevBPP)</td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>1 （黑色和白色）</p></td>
</tr>
<tr class="odd">
<td><p>1</p></td>
<td><p>8</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>24</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p>1 （CMY 和 RGB）</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>1 (<a href="https://msdn.microsoft.com/library/windows/hardware/ff556274#wdkgloss-cmyk" data-raw-source="&lt;em&gt;CMYK&lt;/em&gt;"><em>CMYK</em></a>)</p></td>
</tr>
</tbody>
</table>

 

对于这些格式，可以转换 Unidrv*独立于设备的位图 (DIB)* 到适当的数据设置格式并将其发送到打印机。 (可以对此数据执行的半色调操作中所述[Unidrv 与半色调](halftoning-with-unidrv.md)。)

如果您的打印机支持前面的表中未列出的颜色格式，您必须执行以下操作：

-   设置\*DevNumOfPlanes 和\*DevBPP 属性为零。 执行此操作可防止 Unidrv 将 DIB 数据发送到打印机。

-   提供[呈现插件](rendering-plug-ins.md)实现[ **IPrintOemUni::ImageProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff554261)方法。

[ **IPrintOemUni::ImageProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff554261)方法必须执行以下操作：

-   将 DIB 数据转换为打印机的颜色格式。

-   半色调数据执行操作。

-   将数据发送到打印后台处理程序。

提供有关详细信息[ **IPrintOemUni::ImageProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff554261)函数中，请参阅[自定义颜色格式](customized-color-formats.md)。

### <a name="rendering-high-quality-images"></a>呈现高质量的图像

对于每个颜色格式，您可以指定每个打印机硬件接受的像素的位数和每个你想 Unidrv 创建 Dib 时要使用的像素的位数。 这些值指定与\*DevBPP 和\*DrvBPP 属性，分别。 有时，所以最好图像呈现为位图，具有更多的每像素位数超过打印机可以处理 （按顺序，例如，若要尝试重现高质量的照片）。 因此，它是允许指定\* **DrvBPP**大于相乘的结果的值\* **DevBPP**值\*DevNumOfPlanes 值。

例如，假设你想要定义一种 ColorMode 选项，会将图像呈现为 24 位/像素位图，但然后想要发送到为打印机的位图*CMYK*数据。 您可以定义此模式，如下所示：

```cpp
*Feature: ColorMode
{
    *Option: 24toCMYK
    {
        *Name: "Photographic Quality"
        *DrvBPP: 24
        *DevNumOfPlanes: 4
        *DevBPP: 1
        *ColorPlaneOrder: LIST(CYAN, MAGENTA, YELLOW, BLACK)
        *IPCallbackID: 1
    }
 other options
}
```

在此示例中， \* **DevBPP**并\* **DevNumOfPlanes**属性表示的四个平面，每个平面一位 CMYK 格式 Unidrv 可以呈现，然后发送到打印机。 但是，在这种情况下，半色调操作必须执行在呈现的图像在打印之前。 [微型驱动程序提供半色调](minidriver-supplied-halftoning.md)必须使用。

 

 




