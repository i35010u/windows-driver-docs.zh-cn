---
title: 集成测试
description: 务必执行集成测试，以确保最佳的端到端用户体验。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9fa0ff5ca0aadadab950dd7181e37784e0ee0719
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810049"
---
# <a name="integration-testing"></a>集成测试


务必执行集成测试，以确保最佳的端到端用户体验

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


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
<td align="left"><p><a href="indicator-testing.md" data-raw-source="[Indicator testing](indicator-testing.md)">指示器测试</a></p></td>
<td align="left"><p>本主题介绍常见的指标步骤步骤和示例。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="convertible-testing.md" data-raw-source="[Convertible testing](convertible-testing.md)">变形测试</a></p></td>
<td align="left"><p>本主题介绍改装的测试。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="touchscreen-laptop-system-testing.md" data-raw-source="[Touchscreen laptop system testing](touchscreen-laptop-system-testing.md)">触摸屏笔记本电脑系统测试</a></p></td>
<td align="left"><p>本主题介绍适用于触摸计算机的测试系统。</p></td>
</tr>
</tbody>
</table>

 

每个系统都是唯一的，其实现方式如下：

-   硬件按钮及其位置
-   在改装) 的便携式计算机和石板模式 (之间切换的各种方式

有关本部分中所述的方案的详细信息，请参阅 [Windows 8.1 的 GPIO 按钮和指示器实现指南](gpio-buttons-and-indicators-implementation-guide-for-windows-8-1.md)。

*表1指示器组合预期行为* 显示每个指示器组合的预期行为。

**表1指示器组合预期行为**

| “模式”   | 程序坞     | 显示屏幕键盘 | 已启用自动轮替 |
|--------|----------|-----------------------------|-----------------------|
| 便携式计算机 | 未插接 | 否                          | 否                    |
| 便携式计算机 | 停靠   | 否                          | 否                    |
| 平板  | 未插接 | 是                         | 是                   |
| 平板  | 停靠   | 是                         | 否                    |

 

本部分介绍了涉及停靠和笔记本电脑/石板模式指示器的各种方案的一组测试。 如果任何测试失败，请参阅 [GPIO 日志记录和调查](gpio-logging-and-investigations.md)。

 

 




