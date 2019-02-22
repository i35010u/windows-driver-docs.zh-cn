---
title: 为 Windows 7 的显示器驱动程序设置功能分数
description: 为 Windows 7 的显示器驱动程序设置功能分数
ms.assetid: 7b2cf25d-a88d-48e1-8d62-8c245c289566
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7552c94a24a6eb710fbca980de296c137080d8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543455"
---
# <a name="setting-the-feature-score-for-windows-7-display-drivers"></a>为 Windows 7 的显示器驱动程序设置功能分数


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

**FeatureScore**指令是所必需的所有驱动程序的 Windows Vista 和更高版本操作系统上安装和运行。 中介绍了适用于 Windows Vista 功能分数设置[设置驱动程序功能得分](setting-the-driver-feature-score.md)。 下表显示了功能分数设置适用于 Windows 7 及更高版本。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">功能
<div>
 
</div>
分数</th>
<th align="left">驱动程序模型和分发方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>E6</p></td>
<td align="left"><p>针对该模型进行了优化供应商提供的驱动程序写入到 Windows 显示器驱动程序模型 (WDDM) 的&#39;Windows 的功能打包受限定的 Windows 硬件质量实验室 (WHQL)，将 Windows 7 驱动程序包中还包括在 Windows 中<a href="https://go.microsoft.com/fwlink/p/?linkid=138031" data-raw-source="[Compatibility Center](https://go.microsoft.com/fwlink/p/?linkid=138031)">兼容性中心</a>经过测试的产品列表</p></td>
</tr>
<tr class="even">
<td align="left"><p>E6</p></td>
<td align="left"><p>针对该模型进行了优化供应商提供的驱动程序写入到 WDDM 的&#39;s Windows 7 功能，并附带统一 Windows 7 和 Windows Vista 驱动程序包，通过使用 Windows 硬件认证工具包认证</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EC</p></td>
<td align="left"><p>写入到 WDDM 的现成驱动程序进行了优化模型&#39;s Windows 7 功能，并与 Windows 7 驱动程序包一起打包</p></td>
</tr>
<tr class="even">
<td align="left"><p>F4</p></td>
<td align="left"><p>写入 WDDM 与统一 Windows 7 和 Windows Vista 驱动程序包，通过使用 Windows 硬件认证工具包程序包的证书与供应商提供驱动程序</p></td>
</tr>
<tr class="odd">
<td align="left"><p>F4</p></td>
<td align="left"><p>与 Windows 7 驱动程序包写入 WDDM 的现成驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p>F6</p></td>
<td align="left"><p>供应商提供的驱动程序使用的是由 WHQL 限定，包含在 Windows 的 Windows Vista 驱动程序包写入到 WDDM <a href="https://go.microsoft.com/fwlink/p/?linkid=138031" data-raw-source="[Vista Compatibility Center](https://go.microsoft.com/fwlink/p/?linkid=138031)">Vista 兼容性中心</a>经过测试的产品列表</p></td>
</tr>
<tr class="odd">
<td align="left"><p>F8</p></td>
<td align="left"><p>与 Windows Vista 驱动程序包写入 WDDM 的现成驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p>FC</p></td>
<td align="left"><p>供应商提供的驱动程序写入到<a href="windows-2000-display-driver-model-design-guide.md" data-raw-source="[Windows 2000 display driver model](windows-2000-display-driver-model-design-guide.md)">Windows 2000 显示器驱动程序模型</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>FD</p></td>
<td align="left"><p>在框中将写入到的 Windows Vista 的驱动程序<a href="windows-2000-display-driver-model-design-guide.md" data-raw-source="[Windows 2000 display driver model](windows-2000-display-driver-model-design-guide.md)">Windows 2000 显示器驱动程序模型</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>FE</p></td>
<td align="left"><p>视频图形数组 (VGA) 驱动程序</p></td>
</tr>
</tbody>
</table>

 

有关写入到 WDDM 驱动程序，必须将放置图形硬件供应商**FeatureScore**指令下[ **DDInstall 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344)其 INF 文件和使用**FeatureScore**要应用于驱动程序的特征评分。

有关[Windows 2000 显示器驱动程序模型](windows-2000-display-driver-model-design-guide.md)驱动程序，Microsoft 在现成 Windows 2000 显示器驱动程序模型驱动程序时或在 INF 驱动程序安装的应用通过类安装程序的相应的特征分数。 不能使用供应商**FeatureScore**指令插入到 Windows 2000 显示器驱动程序模型编写的驱动程序的功能分数。

未签名的驱动程序接收功能分数，它等于 FF。 此值是默认值，指示没有分数。

 

 





