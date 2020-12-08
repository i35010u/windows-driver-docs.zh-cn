---
title: 主控单元
description: 主控单元
keywords:
- GPD files WDK Unidrv，主单元
- 主单位 WDK GPD 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ccd4cd379652c306cf7739c482d6e7d8f392182
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807893"
---
# <a name="master-units"></a>主控单元





大多数打印机支持使用各种水平和垂直分辨率的命令。 例如，特定打印机的 "即时换行" 命令可提供一英寸的分辨率： 1/288th 英寸，同时，同一打印机可能支持垂直图形分辨率 1/96th 每英寸。 同样，此打印机还可以提供 1/达到80%、1/160th 和 1/320th 英寸的水平分辨率。

Unidrv 提供了单个坐标系来处理各种不同的解决方案。 此坐标系统中的单位称为 "主单位"。 打印机的主单位表示为 (*x*、 *y*) 对值，其中 *x* 是水平方向的主单元， *y* 是垂直方向的主单位。

若要确定平面的主单位，请为实际分辨率计算分母的最小公倍数 (LCM) 。 使用示例打印机，可以执行以下操作：

-   计算80、160和320的 LCM，即320。 因此，水平母版单位为 1/320th 英寸。

-   计算288和96的 LCM，其为576。 因此，垂直母版单位为 1/576th 英寸。

**重要提示**   主单元值和垂直和水平分辨率应为打印头 (的倍数，即 " **PinsPerPhysPass** " 值) "。 如果不满足此条件，则可能会为某些纸张大小生成额外的空行。

 

若要指定打印机的主单位，请使用 \* *_MasterUnits_* 属性。 该属性的格式如下所示：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>*<strong>MasterUnits</strong>：成对 ( <em>X_Denominator</em> ， <em>Y_Denominator</em> ) </p></td>
</tr>
</tbody>
</table>

 

其中， *X \_ 分母* 是水平分辨率的分母的 lcm， *Y \_ 分母* 是垂直分辨率的分母的 lcm。 以下 GPD 项指定了示例的主单元：

```cpp
*MasterUnits: PAIR(320, 576)
```

通常，必须在主单位中指定 GPD 文件项中使用的位置和大小值。 例如，若要指定我们的示例打印机的最大自定义页面大小为9英寸 x 12 英寸，则使用以下条目，其中 9x320 = 2880 和 12x576 = 6912：

```cpp
*MaxSize: PAIR(2880, 6912)
```

计算主单位的值时，请仅使用希望 Unidrv 支持的设备分辨率。 例如，如果打印机支持水平分辨率 1/达到80%、1/96th 每、1/160th 和 1/320th 英寸，但不打算在96TH 每文件中指定英寸分辨率的 1/GPD，则不要将其包含在 LCM 计算中。

如果你的打印机支持用于移动光标位置的 [cursor 命令](cursor-commands.md)，则在 \* **XMoveUnit** \* 主单位计算中必须包含为 XMoveUnit 和 *_YMoveUnit_*[游标属性](cursor-attributes.md)指定的值。 例如，假设 GPD 文件包含以下条目：

```cpp
*XMoveUnit: 60
*YMoveUnit: 60
```

计算此打印机的主单位时，水平和垂直主单位计算中必须包含一英寸的 1/60th。

 

 




