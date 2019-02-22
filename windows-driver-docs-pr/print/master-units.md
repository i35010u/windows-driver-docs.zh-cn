---
title: 母版单位
description: 母版单位
ms.assetid: 6c3abf16-1206-4b90-a7e9-c8a581191502
keywords:
- GPD 文件 WDK Unidrv，主单位
- 主单位 WDK GPD 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1785ea6c316358d9a991159008bbff3d2ab1a51b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522776"
---
# <a name="master-units"></a>母版单位





大多数打印机支持具有不同的水平和垂直分辨率的命令。 例如，在特定打印机的即时换行符命令可能会提供的分辨率为 1/288th 英寸，而同一打印机可能支持的垂直图形分辨率为 1/96th 每英寸为单位。 同样，这台打印机可能还会提供水平分辨率为 1/80th、 1 / 160th，和 1/320th 1/96 英寸为单位。

Unidrv 提供单一的坐标系统来处理这些不同的分辨率。 此坐标系统中的单元是名为 master 的单位。 打印机的主单位表示为 (*x*， *y*) 对的值，其中*x*是水平方向的主单位和*y*是垂直方向的主单位。

若要确定一个平面主单位，计算最小公倍数 (LCM) 的实际分辨率为分母。 使用示例打印机，请执行以下操作：

-   计算 80、 160 和 320，的 LCM 是 320。 因此，水平的主计价单位为 1/320th 1/96 英寸为单位。

-   计算 LCM 288 和 96，这是 576。 因此，垂直主单位为 1/576th 1/96 英寸为单位。

**重要**  这两个主单元值和垂直和水平分辨率应为打印头中的 pin 数的倍数 (即**PinsPerPhysPass**值)。 如果不满足此条件，就可以额外的空白的行，将生成适用于特定纸张大小。

 

若要指定打印机的主单元，请使用\* **MasterUnits**属性。 该特性的格式如下所示：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>*<strong>MasterUnits</strong>:PAIR ( <em>X_Denominator</em> , <em>Y_Denominator</em> )</p></td>
</tr>
</tbody>
</table>

 

其中*X\_分母*是针对水平分辨率，分母，LCM 和*Y\_分母*是针对垂直分辨率分母，LCM。 以下 GPD 条目指定的主单位。 例如：

```cpp
*MasterUnits: PAIR(320, 576)
```

通常情况下，必须以 master 为单位指定位置和 GPD 文件条目中使用的大小值。 例如，若要指定我们示例中的打印机的最大自定义页面大小是 9 英寸 × 12 英寸的以下条目会使用，其中 9 x 320 = 2880 和 12 x 576 = 6912:

```cpp
*MaxSize: PAIR(2880, 6912)
```

当主单位的计算值，使用想 Unidrv 以支持设备分辨率。 例如，如果打印机支持水平分辨率为 1/达到 80，1/96，1/160th，到 1/320th 英寸，但不是打算指定 1/96th 每英寸解析在 GPD 文件中，不包括该 LCM 计算中。

如果打印机支持[游标命令](cursor-commands.md)移动光标位置，然后为指定值\* **XMoveUnit**并\* **YMoveUnit**[游标属性](cursor-attributes.md)必须包括在主单元计算。 例如，假设 GPD 文件包含以下各项：

```cpp
*XMoveUnit: 60
*YMoveUnit: 60
```

当计算此打印机的主单元，1/英寸为单位的 60th 必须包括在水平和垂直主单元计算。

 

 




