---
title: 设置 Windows 7 显示驱动程序的功能评分
description: 设置 Windows 7 显示驱动程序的功能评分
ms.assetid: 7b2cf25d-a88d-48e1-8d62-8c245c289566
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 055dcf0f7133e3b0021b9ee5035a729c67713a16
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365556"
---
# <a name="setting-the-feature-score-for-windows-7-display-drivers"></a>设置 Windows 7 显示驱动程序的功能评分


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
score</th>
<th align="left">驱动程序模型和分发方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>E6</p></td>
<td align="left"><p>供应商提供的驱动程序写入到 Windows 显示器驱动程序模型 (WDDM) 的针对模型的 Windows 7 功能进行了优化，受限定的 Windows 硬件质量实验室 (WHQL)，将 Windows 7 驱动程序包中打包，并且包含在Windows<a href="https://go.microsoft.com/fwlink/p/?linkid=138031" data-raw-source="[Compatibility Center](https://go.microsoft.com/fwlink/p/?linkid=138031)">兼容性中心</a>经过测试的产品列表</p></td>
</tr>
<tr class="even">
<td align="left"><p>E6</p></td>
<td align="left"><p>供应商提供的驱动程序写入到 WDDM 针对模型的 Windows 7 功能进行了优化，并打包了统一的 Windows 7 和 Windows Vista 驱动程序包，通过使用 Windows 硬件认证工具包认证</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EC</p></td>
<td align="left"><p>写入到 WDDM 的现成驱动程序模型的 Windows 7 功能进行了优化，与 Windows 7 驱动程序包打包在一起</p></td>
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

 

有关写入到 WDDM 驱动程序，必须将放置图形硬件供应商**FeatureScore**指令下[ **DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)其 INF 文件和使用**FeatureScore**要应用于驱动程序的特征评分。

有关[Windows 2000 显示器驱动程序模型](windows-2000-display-driver-model-design-guide.md)驱动程序，Microsoft 在现成 Windows 2000 显示器驱动程序模型驱动程序时或在 INF 驱动程序安装的应用通过类安装程序的相应的特征分数。 不能使用供应商**FeatureScore**指令插入到 Windows 2000 显示器驱动程序模型编写的驱动程序的功能分数。

未签名的驱动程序接收功能分数，它等于 FF。 此值是默认值，指示没有分数。

 

 





