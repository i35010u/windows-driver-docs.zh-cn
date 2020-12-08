---
title: 按钮报告
description: 基于在按钮数组的已定义 GPIO 资源上收到的中断，内置常规用途 i/o (GPIO) 按钮驱动程序向 Windows 报告。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a538d70f60d786b002eeb66098eaeb1d64069c2d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827171"
---
# <a name="button-reporting"></a>按钮报告


基于在按钮数组的已定义 GPIO 资源上收到的中断，内置常规用途 i/o (GPIO) 按钮驱动程序向 Windows 报告。

内置的 GPIO 按钮驱动程序报告 *表 1 GPIO 按钮报告* 中列出的按钮按下和组合。

**表 1 GPIO 按钮报告**

| Button        | 需要 \_ CRS 已唤醒 | 需要在 SOC 上安装 | 边缘报表 (假设 ActiveLow)  |
|---------------|-------------------------|----------------------|-------------------------------------|
| Windows       | 是                     | 是                  | 双向                                |
| 调高音量     | 是                     | 是                  | 双向                                |
| 减小音量   | 是                     | 是                  | 双向                                |
| 旋转锁定 | 否                      | 是                  | 双向                                |
| 强力         | 是                     | 是                  | 双向                                |

 

所有非 GPIO 基于的实现必须遵循相同的报告方案。

定义顺序为 "电源"、"Windows"、"音量增加"、"音量减少" 和 "旋转锁定"。 有关如何为这些类创建 HID 描述符的示例，请参阅 [hid 按钮报告描述符](hid-button-report-descriptors.md)。

**注意**  
以前的要求描述了使用 **Win + O** 进行旋转锁定。 尽管此组合仍然起作用，但它并不受键盘布局更改，而 **Win + F14** 是不可知的。

 

**表2非 GPIO 按钮的报表触发器**

| 单个按钮报告 | Source              | 用法要求      | 报表触发器         | 重复 |
|-----------------------------|---------------------|-------------------------|------------------------|----------|
| 强力                       | 系统控制      | 0x84 (Power)             | 物理按钮–向上键   | 否       |
| Windows                     | Keyboard            | 0xE3 (Win)               | 物理按钮–向上键   | 否       |
| 调高音量                   | 使用者集合 | 0xE9 (容量)         | 物理按钮–按下 | 是      |
| 减小音量                 | 使用者集合 | 0xEA (音量降低)       | 物理按钮–按下 | 是      |
| 旋转锁定               | Keyboard            | 0xE3 = 0x69 (Win + F14)  | 物理按钮–按下 | 否       |

 

以下键盘组合必须根据其完成情况进行报告，如果组合已保留，则不应重复此组合。

**表3非 GPIO 按钮组合的报表触发器**

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
<th align="left">用法要求</th>
<th align="left">报表触发器</th>
<th align="left">重复</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Windows + 电源</td>
<td align="left"><p>0xE0 + 0xE2 + 0x4C</p>
<p> (<strong>Ctrl + Alt + Del</strong>) </p></td>
<td align="left">物理电源按钮–按下</td>
<td align="left">否</td>
</tr>
<tr class="even">
<td align="left">Windows + 音量向上</td>
<td align="left"><p>0xE3 + 0xE0 + 0x69</p>
<p> (<strong>Win + Ctrl + F14</strong>) </p></td>
<td align="left">物理音量按钮-Down</td>
<td align="left">否</td>
</tr>
<tr class="odd">
<td align="left">Windows + 向下音量</td>
<td align="left"><p>0xE3 + 0x6A</p>
<p> (<strong>Win + F15</strong>) </p></td>
<td align="left">物理音量按钮-Down</td>
<td align="left">否</td>
</tr>
</tbody>
</table>

 

**注意**  
-   有关电源按钮的完整指导和实现，请参阅 [电源按钮行为和实现](/collaborate/connect-redirect?DownloadID=47452)。
-   有关按钮的连接备用指南，请参阅 [连接备用唤醒源](/collaborate/connect-redirect?DownloadID=49891)。
-   有关 ACPI 实现的其他指导，请参阅 [Acpi 设计指南](/collaborate/connect-redirect?DownloadID=48755)。

 

 

