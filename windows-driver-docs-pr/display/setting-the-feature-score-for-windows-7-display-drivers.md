---
title: 设置 Windows 7 显示驱动程序的功能评分
description: 设置 Windows 7 显示驱动程序的功能评分
ms.assetid: 7b2cf25d-a88d-48e1-8d62-8c245c289566
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac3ebf1d6c3f1fcce2c91b0a0f948da660d6ba00
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066636"
---
# <a name="setting-the-feature-score-for-windows-7-display-drivers"></a>设置 Windows 7 显示驱动程序的功能评分


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

在 Windows Vista 及更高版本的操作系统上安装和运行的所有驱动程序都需要 **FeatureScore** 指令。 适用于 Windows Vista 的功能分数设置在 [设置驱动程序功能分数](setting-the-driver-feature-score.md)中进行了介绍。 下表显示适用于 Windows 7 和更高版本的功能分数设置。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Feature
<div>
 
</div>
score</th>
<th align="left">驱动程序型号和分发方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>E6</p></td>
<td align="left"><p>写入到 Windows 显示驱动程序模型 (WDDM) 的供应商提供的驱动程序已针对该模型的 Windows 7 功能进行了优化，这些驱动程序包已打包在 windows 硬件质量实验室 (WHQL) 所限定的 Windows 7 驱动程序包中，并包括在 Windows <a href="https://go.microsoft.com/fwlink/p/?linkid=138031" data-raw-source="[Compatibility Center](https://go.microsoft.com/fwlink/p/?linkid=138031)">兼容性中心</a> 测试的产品列表中</p></td>
</tr>
<tr class="even">
<td align="left"><p>E6</p></td>
<td align="left"><p>写入 WDDM 的供应商提供的驱动程序针对该模型的 Windows 7 功能进行了优化，并与通过使用 Windows 硬件认证工具包认证的统一 Windows 7 和 Windows Vista 驱动程序包一起打包</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EC</p></td>
<td align="left"><p>写入 WDDM 的内置驱动程序针对该模型的 Windows 7 功能进行了优化，并与 Windows 7 驱动程序包一起打包</p></td>
</tr>
<tr class="even">
<td align="left"><p>F4</p></td>
<td align="left"><p>供应商提供的驱动程序，使用统一的 Windows 7 和 Windows Vista 驱动程序包写入到 WDDM，并使用 Windows 硬件认证工具包对包进行认证</p></td>
</tr>
<tr class="odd">
<td align="left"><p>F4</p></td>
<td align="left"><p>使用 Windows 7 驱动程序包写入 WDDM 的内置驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p>F6</p></td>
<td align="left"><p>供应商提供的驱动程序，这些驱动程序使用 Windows Vista 驱动程序包（由 WHQL 限定并包含在 Windows <a href="https://go.microsoft.com/fwlink/p/?linkid=138031" data-raw-source="[Vista Compatibility Center](https://go.microsoft.com/fwlink/p/?linkid=138031)">Vista 兼容性中心</a> 测试的产品列表）写入 WDDM</p></td>
</tr>
<tr class="odd">
<td align="left"><p>F8</p></td>
<td align="left"><p>使用 Windows Vista 驱动程序包写入到 WDDM 的内置驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p>FC</p></td>
<td align="left"><p>写入到<a href="windows-2000-display-driver-model-design-guide.md" data-raw-source="[Windows 2000 display driver model](windows-2000-display-driver-model-design-guide.md)">Windows 2000 显示器驱动程序模型</a>中的供应商提供的驱动程序</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FD</p></td>
<td align="left"><p>Windows Vista 中写入<a href="windows-2000-display-driver-model-design-guide.md" data-raw-source="[Windows 2000 display driver model](windows-2000-display-driver-model-design-guide.md)">windows 2000 显示器驱动程序模型</a>的内置驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p>FE</p></td>
<td align="left"><p>视频图形阵列 (VGA) 驱动程序</p></td>
</tr>
</tbody>
</table>

 

对于写入 WDDM 的驱动程序，图形硬件供应商必须将 **FeatureScore** 指令放在其 INF 文件的 [**DDInstall 部分**](../install/inf-ddinstall-section.md) 下，并使用 **FeatureScore** 将功能分数应用于驱动程序。

对于 [Windows 2000 显示器驱动程序模型](windows-2000-display-driver-model-design-guide.md) 驱动程序，Microsoft 会在安装驱动程序时通过类安装程序来应用相应的功能分数，或在用于内置 Windows 2000 显示驱动程序模型驱动程序的 INF 中应用相应的功能分数。 供应商不得使用 **FeatureScore** 指令为写入 Windows 2000 显示驱动程序模型的驱动程序插入功能分数。

未签名的驱动程序接收的功能分数等于 FF。 此值为默认值，表示没有评分。

 

