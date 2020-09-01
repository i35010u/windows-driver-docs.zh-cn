---
title: ProcAmp 属性
description: ProcAmp 属性
ms.assetid: 412c9144-dd52-4b36-bea1-b17c9c2c95b3
keywords:
- ProcAmp WDK DirectX VA，属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 111248c032d2b79f14bea32e8956582a53879727
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066446"
---
# <a name="procamp-properties"></a>ProcAmp 属性


## <span id="ddk_procamp_properties_gg"></span><span id="DDK_PROCAMP_PROPERTIES_GG"></span>


当 VMR 查询驱动程序以获取有关 ProcAmp 属性的信息时，显示驱动程序必须提供最小值、最大值、步长大小和默认值。 驱动程序可以提供此信息，以响应对其 [**ProcAmpControlQueryRange**](./dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange.md) 函数的调用。 尽管驱动程序可以返回 ProcAmp 属性的任何值，但以下是建议的设置， (所有值都) 浮动。

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
<th align="left">properties</th>
<th align="left">最小值</th>
<th align="left">最大值</th>
<th align="left">默认</th>
<th align="left">增量</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>亮度</p></td>
<td align="left"><p>-100.0 f</p></td>
<td align="left"><p>100.0 f</p></td>
<td align="left"><p>0.0F</p></td>
<td align="left"><p>0.1 f</p></td>
</tr>
<tr class="even">
<td align="left"><p>与此示例</p></td>
<td align="left"><p>0.0F</p></td>
<td align="left"><p>10.0 f</p></td>
<td align="left"><p>1.0 f</p></td>
<td align="left"><p>0.01 f</p></td>
</tr>
<tr class="odd">
<td align="left"><p>饱和度</p></td>
<td align="left"><p>0.0F</p></td>
<td align="left"><p>10.0 f</p></td>
<td align="left"><p>1.0 f</p></td>
<td align="left"><p>0.01 f</p></td>
</tr>
<tr class="even">
<td align="left"><p>色调</p></td>
<td align="left"><p>-180.0 f</p></td>
<td align="left"><p>180.0 f</p></td>
<td align="left"><p>0.0F</p></td>
<td align="left"><p>0.1 f</p></td>
</tr>
</tbody>
</table>

 

如果默认值导致视频流的转换为 *null* ，则这一点非常重要。 这允许 VMR 在应用程序未更改任何 ProcAmp 控件属性时，绕过其视频管道中的 ProcAmp 调整阶段。

使用 ProcAmp 属性时，VMR 和显示驱动程序将执行某些验证。 VMR 在调用驱动程序之前强制执行以下参数验证：

-   VMR 确保应用程序提供的值位于驱动程序指定的有效范围内。 VMR 将任何应用程序提供的值夹紧到指定范围。 例如，如果亮度的最大值为100，并且应用程序提供的值为105，则 VMR 会将该应用程序的值夹紧为100。 当应用程序查询 VMR 来确定当前亮度设置时，它会收到限制值，在本例中为100。

-   VMR 还会对应用程序提供的值进行任何必要的舍入，以确保值位于由驱动程序返回的步长大小增量所指示的最近位置。 例如，如果亮度步长的增量为0.5，则允许的最小亮度值为-100.0，并且应用程序提供值-80.7。 在此示例中，VMR 将应用程序的值调整为最接近的有效值-80.5。

驱动程序应确保以下关系保持：

-   最大范围值大于最小范围值。 这表示最大值和最小值之间的差值大于0.0。

-   默认值和最大值位于步长大小增量指定的有效位置上，如下面的表达式所示：
    ```cpp
    min + (int((default - min) / increment) * increment) == default
    min + (int((max - min) / increment) * increment) == max
    ```

-   由于应用程序通常使用 Windows 的滑块控件来显示 ProcAmp 设置，并且由于 Windows 滑块控件的最大范围为65536，因此驱动程序应将不同 ProcAmp 值的数目保持在65536的范围内。 对于所选的值，以下不相等应为 true：
    ```cpp
    int((max - min) / increment) < 65536.
    ```

-   对于你的硬件不支持的 ProcAmp 属性，驱动程序应返回步长大小增量为0.0 的 "最大值"、"最小值" 和 "默认值"。

 

