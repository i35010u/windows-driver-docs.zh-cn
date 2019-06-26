---
title: 按钮报告
description: 在框通用 I/O (GPIO) 按钮驱动程序报告给 Windows，基于的按钮数组定义的 GPIO 资源接收的中断。
ms.assetid: 7D96E1CB-3406-4D61-9D5C-65BC6BFD1FFA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3850e9d4e623abf71b21064d7732c3b99a8917ed
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385168"
---
# <a name="button-reporting"></a>按钮报告


在框通用 I/O (GPIO) 按钮驱动程序报告给 Windows，基于的按钮数组定义的 GPIO 资源接收的中断。

在框 GPIO 按钮驱动程序报告的按钮，按下和中列出的组合*表 1 GPIO 按钮 Reporting*。

**表 1 GPIO 按钮报告**

| Button        | 需要\_CRS 可唤醒 | 需要在 SOC GPIO | 边缘 Reporting (假定 ActiveLow) |
|---------------|-------------------------|----------------------|-------------------------------------|
| Windows       | 是                     | 是                  | 两者                                |
| 调高音量     | 是                     | 是                  | 两者                                |
| 减小音量   | 是                     | 是                  | 两者                                |
| 旋转锁 | 否                      | 是                  | 两者                                |
| 电源         | 是                     | 是                  | 两者                                |

 

所有非基于 GPIO 实现必须遵循相同的报告方案。

定义的顺序是电源、 Windows、 音量、 音量减小和旋转锁。 有关如何创建针对这些 HID 描述符的示例，请参阅[HID 按钮报告描述符](hid-button-report-descriptors.md)。

**请注意**  介绍了如何使用上一步要求**Win + O**旋转锁。 尽管这种组合是仍正常工作，但不受键盘布局更改，而**Win + F14**是不可知的布局。

 

**表 2 会触发报告非 GPIO 按钮**

| 个别按钮报告 | Source              | 使用要求      | 报表触发器         | 重复 |
|-----------------------------|---------------------|-------------------------|------------------------|----------|
| 电源                       | 系统控制      | 0x84 （电源）            | 物理按钮 – 向上一级   | 否       |
| Windows                     | 键盘            | 0xE3 (Win)              | 物理按钮 – 向上一级   | 否       |
| 调高音量                   | 使用者集合 | 0xE9 （调高音量）        | 物理按钮 – 向下 | 是      |
| 减小音量                 | 使用者集合 | 0xEA （向下的卷）      | 物理按钮 – 向下 | 是      |
| 旋转锁               | 键盘            | 0xE3 = 0x69 (Win + F14) | 物理按钮 – 向下 | 否       |

 

以下键盘组合必须被报告基于其完成时，并且不应如果保留组合重复。

**表 3 会触发报告为非-GPIO 按钮组合**

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">按钮组合报告</th>
<th align="left">使用要求</th>
<th align="left">报表触发器</th>
<th align="left">重复</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Windows + 电源</td>
<td align="left"><p>0xE0 + 0xE2 + 0x4C</p>
<p>(<strong>Ctrl + Alt + Del</strong>)</p></td>
<td align="left">物理电源按钮 – 向下</td>
<td align="left">否</td>
</tr>
<tr class="even">
<td align="left">Windows + 调高音量</td>
<td align="left"><p>0xE3 + 0xE0 + 0x69</p>
<p>(<strong>Win + Ctrl + F14</strong>)</p></td>
<td align="left">物理卷按钮的向下</td>
<td align="left">否</td>
</tr>
<tr class="odd">
<td align="left">Windows + 向下的卷</td>
<td align="left"><p>0xE3 + 0x6A</p>
<p>(<strong>Win + F15</strong>)</p></td>
<td align="left">物理卷按钮的向下</td>
<td align="left">否</td>
</tr>
</tbody>
</table>

 

**注意**  
-   有关完整的指导和实现的电源按钮，请参阅[电源按钮行为和实现](https://aka.ms/connect-redirect?DownloadID=47452)。
-   连接待机按钮的指南，请参阅[连接待机状态唤醒的源](https://aka.ms/connect-redirect?DownloadID=49891)。
-   ACPI 实现的其他指南，请参阅[ACPI 设计指南](https://aka.ms/connect-redirect?DownloadID=48755)。

 

 

 




