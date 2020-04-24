---
ms.assetid: EB2264A4-BAE8-446B-B9A5-19893936DDCA
title: 驱动程序参考页的目标平台
description: 在 Microsoft 驱动程序参考页底部的“要求”块中，将看到一个称为“目标平台”的条目。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bf53562619c2fff7f444a36373553cc7f5b6b70
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "63344040"
---
# <a name="target-platform-on-driver-reference-pages"></a>驱动程序参考页上的“目标平台”

在 Microsoft 驱动程序参考页底部的“要求”块中，将看到一个称为“目标平台”  的条目。 该行列出了页面将应用到的 Windows 版本。

以下是此类条目的示例：

![目标平台在“要求”块中设置为“通用”](images/TargetPlatform.png)

在**目标平台**中指定的值将映射到可在 Visual Studio 中使用的值（在“配置属性”-&gt;“驱动程序设置”-&gt;“常规”  下的“目标平台”  属性中）。

以下是你可能看到的**目标平台**的值以及它们的含义：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Universal"></span><span id="universal"></span><span id="UNIVERSAL"></span>通用</p></td>
<td align="left"><p>通用 Windows 驱动程序的驱动程序二进制文件可以调用此设备驱动程序接口 (DDI)。</p>
<p>通用 Windows 驱动程序在以下基于通用 Windows 平台 (UWP) 的 Windows 10 版本上运行：</p>
<ul>
<li>Windows 10 桌面版（家庭版、专业版和企业版）</li>
<li>处于 S 模式的 Windows 10</li>
<li>Windows 10 移动版</li>
<li>Windows 10 IoT 核心版</li>
<li>Windows Server 2016</li>
</ul>
<p>有关详细信息，请参阅<a href="getting-started-with-universal-drivers.md" data-raw-source="[Getting Started with Universal Windows drivers](getting-started-with-universal-drivers.md)">通用 Windows 驱动程序入门</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Desktop"></span><span id="desktop"></span><span id="DESKTOP"></span>桌面版</p></td>
<td align="left"><p>Windows 10 桌面版或 Windows Server 2016 的驱动程序二进制文件可以调用此 DDI。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Mobile"></span><span id="mobile"></span><span id="MOBILE"></span>移动版</p></td>
<td align="left"><p>Windows 10 移动版的驱动程序二进制文件可以调用此 DDI。</p></td>
</tr>
</tbody>
</table>

 

 

 





