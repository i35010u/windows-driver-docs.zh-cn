---
title: ProcAmp 属性
description: ProcAmp 属性
ms.assetid: 412c9144-dd52-4b36-bea1-b17c9c2c95b3
keywords:
- ProcAmp WDK DirectX VA 属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 399d2975d06360626c3590cd247b951cdea6d590
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352187"
---
# <a name="procamp-properties"></a>ProcAmp 属性


## <span id="ddk_procamp_properties_gg"></span><span id="DDK_PROCAMP_PROPERTIES_GG"></span>


当 VMR 查询 ProcAmp 属性信息的驱动程序时，显示器驱动程序必须提供最小值、 最大值、 步长、 和默认值。 该驱动程序可以提供此信息以响应对的调用其[ **ProcAmpControlQueryRange** ](https://msdn.microsoft.com/library/windows/hardware/ff563950)函数。 尽管该驱动程序可以返回 ProcAmp 属性的任何值，以下是建议的设置 （所有值都是浮点数）。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">最低要求</th>
<th align="left">最多</th>
<th align="left">默认</th>
<th align="left">增量</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>亮度</p></td>
<td align="left"><p>-100.0F</p></td>
<td align="left"><p>100.0F</p></td>
<td align="left"><p>0.0F</p></td>
<td align="left"><p>0.1F</p></td>
</tr>
<tr class="even">
<td align="left"><p>与此示例</p></td>
<td align="left"><p>0.0F</p></td>
<td align="left"><p>10.0F</p></td>
<td align="left"><p>1.0F</p></td>
<td align="left"><p>0.01F</p></td>
</tr>
<tr class="odd">
<td align="left"><p>饱和度</p></td>
<td align="left"><p>0.0F</p></td>
<td align="left"><p>10.0F</p></td>
<td align="left"><p>1.0F</p></td>
<td align="left"><p>0.01F</p></td>
</tr>
<tr class="even">
<td align="left"><p>色调</p></td>
<td align="left"><p>-180.0F</p></td>
<td align="left"><p>180.0F</p></td>
<td align="left"><p>0.0F</p></td>
<td align="left"><p>0.1F</p></td>
</tr>
</tbody>
</table>

 

非常重要，默认值将导致*null*视频流的转换。 这允许 VMR 绕过其视频管道中的 ProcAmp 调整阶段，如果应用程序未更改任何 ProcAmp 控件属性。

VMR 和显示器驱动程序时使用 ProcAmp 属性执行某些验证。 VMR 调用驱动程序之前强制实施以下参数验证：

-   VMR 可确保由应用程序提供的值在由驱动程序指定有效的范围内。 VMR 固定到指定范围内的任何应用程序提供值。 例如，如果亮度的最大值为 100，且应用程序提供的值为 105，VMR 固定至 100 之间的应用程序的值。 当应用程序查询 VMR 来确定当前亮度设置时，它接收的限制的值，在这种情况下 100。

-   VMR 还可进行任何必要舍入为应用程序提供值，以确保由您的驱动程序返回步骤大小增量值落在最近的位置。 例如，如果亮度步骤大小增量为 0.5，最小允许的亮度值是-100.0 次，而应用程序提供-80.7 的值。 VMR 调整到的应用程序的值接近有效的值，在此情况下-80.5。

该驱动程序应确保以下关系保存：

-   最大范围值大于最小范围值。 这意味着，最大和最小值之间的区别是大于 0.0。

-   以下表达式中所示，默认和最大值落在由步骤大小递增，指定有效的位置上：
    ```cpp
    min + (int((default - min) / increment) * increment) == default
    min + (int((max - min) / increment) * increment) == max
    ```

-   由于应用程序通常使用 Windows 的滑块控件来显示 ProcAmp 设置和控制的 Windows 的最大范围滑块，因此为 65536，驱动程序应保存为少于 65536 ProcAmp 的非重复值数。 以下不等应为选择的值，则返回 true:
    ```cpp
    int((max - min) / increment) < 65536.
    ```

-   对于不受您的硬件的 ProcAmp 属性，则驱动程序应返回的最大值、 最小值和默认值为 0.0 步骤大小增量。

 

 





