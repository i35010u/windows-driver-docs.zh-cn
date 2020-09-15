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
ms.openlocfilehash: 11ffa04f71cf341131290f5debaa30f0a7fbf4e7
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106334"
---
# <a name="handling-color-formats"></a>处理颜色格式





打印机支持的每种颜色格式被指定为 ColorMode 功能的选项。 通过使用 [ColorMode 功能的选项属性](option-attributes-for-the-colormode-feature.md)，可以描述打印机所能接受的每种颜色格式。 下表说明了 Unidrv 可以处理的颜色数据格式。

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
<td>在设备 (<em> DevNumOfPlanes) </td>
<td>在设备 (</em> DevBPP) </td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>1 (黑色和白色) </p></td>
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
<td><p>1 (CMY 和 RGB) </p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p>1 (<a href="/windows-hardware/drivers/#wdkgloss-cmyk" data-raw-source="&lt;em&gt;CMYK&lt;/em&gt;"><em>CMYK</em></a>) </p></td>
</tr>
</tbody>
</table>

 

对于这些格式，Unidrv 可以将 *与设备无关的位图 () DIB * 转换为正确的格式，并将其发送到打印机。 在 [Unidrv](halftoning-with-unidrv.md)中，可以对此数据执行的 (半色调运算。 ) 

如果打印机支持上表中未列出的颜色格式，则必须执行以下操作：

-   将 \* DevNumOfPlanes 和 \* DevBPP 属性设置为零。 这样做可以防止 Unidrv 将 DIB 数据发送到打印机。

-   提供实现[**IPrintOemUni：： ImageProcessing**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)方法的[呈现插件](rendering-plug-ins.md)。

[**IPrintOemUni：： ImageProcessing**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)方法必须执行以下操作：

-   将 DIB 数据转换为打印机的颜色格式。

-   对数据执行半色调运算。

-   将数据发送到打印后台处理程序。

有关提供 [**IPrintOemUni：： ImageProcessing**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing) 函数的详细信息，请参阅 [自定义颜色格式](customized-color-formats.md)。

### <a name="rendering-high-quality-images"></a>呈现高质量映像

对于每个颜色格式，你都可以指定打印机硬件接受的每个像素的位数，以及你希望 Unidrv 在创建 Dib 时使用的每个像素的位数。 这些值 \* 分别与 DevBPP 和 \* DrvBPP 特性一起指定。 有时，图像需要呈现为位图，每个像素的位数越高，而打印机可以按顺序处理 (，例如，尝试复制高质量的照片) 。 因此，允许指定的 \* **DrvBPP**值大于 \* **DevBPP**值乘以 DevNumOfPlanes 值所得的结果 \* 。

例如，假设要定义一个 ColorMode 选项，该选项会使图像呈现为24位/像素位图，但随后需要将位图作为 *CMYK* 数据发送到打印机。 可以按如下所示定义此模式：

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

在此示例中， \* **DevBPP**和 \* **DevNumOfPlanes**属性表示 Unidrv 可呈现并发送到打印机的四个平面的每个平面 CMYK 格式。 但是，在这种情况下，必须在呈现的图像上执行半色调操作才能进行打印。 必须使用[微型驱动程序提供的半色调](minidriver-supplied-halftoning.md)。

