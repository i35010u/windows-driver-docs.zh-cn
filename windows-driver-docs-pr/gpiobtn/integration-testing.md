---
title: 集成测试
description: 请务必执行集成测试，以确保最佳的端到端用户体验。
ms.assetid: 61C1AC15-498B-432B-8D26-0303425114FF
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fbddea454f0fdd56f4f159d6fcb79ebb6df99cd0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542795"
---
# <a name="integration-testing"></a>集成测试


务必要执行测试，以确保最佳的端到端用户体验的集成

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>在本部分中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="indicator-testing.md" data-raw-source="[Indicator testing](indicator-testing.md)">测试指示器</a></p></td>
<td align="left"><p>本主题介绍常见指示器步骤过程和示例。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="convertible-testing.md" data-raw-source="[Convertible testing](convertible-testing.md)">转换测试</a></p></td>
<td align="left"><p>本主题介绍针对双用型测试。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="touchscreen-laptop-system-testing.md" data-raw-source="[Touchscreen laptop system testing](touchscreen-laptop-system-testing.md)">触摸屏便携式计算机系统测试</a></p></td>
<td align="left"><p>本主题介绍针对触摸屏便携式计算机系统测试。</p></td>
</tr>
</tbody>
</table>

 

每个系统中是唯一的实现以下的方式：

-   硬件按钮和它们的位置
-   便携式计算机和 （适用于双用型） 的盖板模式之间切换的各种方法

在本部分中所述的方案的详细信息，请参阅[Windows 8.1 的 GPIO 按钮和指示器实施指南](gpio-buttons-and-indicators-implementation-guide-for-windows-8-1.md)。

*表 1 指示器组合预期行为*显示每个指示器组合的预期的行为。

**表 1 指示器组合预期行为**

| 模式   | 靠接     | 显示屏幕键盘 | 启用自动轮换 |
|--------|----------|-----------------------------|-----------------------|
| 便携式计算机 | 取消停靠 | 否                          | 否                    |
| 便携式计算机 | 停靠   | 否                          | 否                    |
| 静态图像  | 取消停靠 | 是                         | 是                   |
| 静态图像  | 停靠   | 是                         | 否                    |

 

本部分介绍一系列涉及停靠和便携式计算机/盖板模式指示器的各种方案的测试。 如果任何测试失败，请参阅[GPIO 日志记录和调查](gpio-logging-and-investigations.md)。

 

 




