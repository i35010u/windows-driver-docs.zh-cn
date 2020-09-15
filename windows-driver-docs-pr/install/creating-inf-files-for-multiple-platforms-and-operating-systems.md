---
title: 创建适用于多个平台和操作系统的 INF 文件
description: 创建适用于多个平台和操作系统的 INF 文件
ms.assetid: 61996c72-c5a7-4ff0-aeb3-6e77b77542c8
keywords:
- INF 文件 WDK 设备安装、多个平台和操作系统
- 多个操作系统 WDK、INF 文件
- 跨平台 INF 文件 WDK
- 操作系统 WDK，互操作系统 INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c365d259e495b192e0eed3f00016be991ca3619
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103458"
---
# <a name="creating-inf-files-for-multiple-platforms-and-operating-systems"></a>创建适用于多个平台和操作系统的 INF 文件





通过对 [inf 文件部分和指令](./index.md)使用系统定义的平台扩展，可以为跨平台安装创建单个 INF 文件。 扩展使你能够创建 *修饰* 的部分名称，这些名称指定哪些节和指令与每个目标平台和操作系统相关。 例如，你可以创建一个 INF 文件，该文件只能在基于 x64 的系统上安装设备，只能在基于 x86 的系统上安装，也可以在 Windows 2000 和更高版本的 Windows 支持的所有系统上安装。

下表汇总了可添加到支持扩展的节的名称的系统支持的平台扩展。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">平台扩展</th>
<th align="left">使用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>.ntamd64</strong></p></td>
<td align="left"><p>本部分包含有关在 Windows XP 和更高版本支持的基于 x64 的系统上安装设备或设备兼容模型集的说明。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.ntia64</strong></p></td>
<td align="left"><p>本部分包含有关在 Windows XP 和更高版本支持的基于 Itanium 的系统上安装设备或设备兼容模型集的说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>.ntx86</strong></p></td>
<td align="left"><p>本部分包含有关在 Windows XP 和更高版本支持的基于 x86 的系统上安装设备或设备兼容模型集的说明。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.ntarm</strong></p></td>
<td align="left"><p>本部分包含有关在基于 ARM 的系统上安装 Windows 8 及更高版本支持的设备或设备兼容模型集的说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>.ntarm64</strong></p></td>
<td align="left"><p>本部分包含有关在基于 ARM64 的系统上安装 Windows 10 版本1709及更高版本支持的设备或设备兼容模型集的说明。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>。 nt</strong></p></td>
<td align="left"><p>在早于 Windows Server 2003 SP1 的 Windows 版本中，部分包含有关在操作系统支持的所有系统上安装设备或设备兼容模型集的说明。</p>
<p>从 Windows Server 2003 SP1 开始，部分包含有关在操作系统支持的基于 x86 的系统上安装设备或设备兼容模型集的说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>不 (平台扩展) </p></td>
<td align="left"><p>在早于 Windows Server 2003 SP1 的 Windows 版本中，部分包含有关在操作系统支持的所有系统上安装设备或设备兼容模型集的说明。</p>
<p>从 Windows Server 2003 SP1 开始，部分包含有关在操作系统支持的基于 x86 的系统上安装设备或设备兼容模型集的说明。</p></td>
</tr>
</tbody>
</table>

 

**重要提示**   从 Windows Server 2003 SP1 开始，INF 文件必须用来修饰 " [**Inf 模型" 部分**](inf-models-section.md)中的条目。**ntia64**、。**ntarm**、。**ntarm64**或。用于指定非 x86 目标操作系统版本的**ntamd64**平台扩展。 对于基于 x86 的目标操作系统版本或非 PnP 驱动程序 INF 文件，这些平台扩展在 INF 文件中不是必需的 (例如，基于 x64 的体系结构的文件系统驱动程序 INF 文件) 。

 

**提示**  我们强烈建议你始终在 [**INF 模型部分**](inf-models-section.md) 中为 windows XP 和更高版本 windows 的目标操作系统的平台扩展修饰条目。 对于基于 x86 的硬件平台，应避免使用 **nt** 平台扩展，并改为使用 **ntx86** 。

 

## <a name="in-this-section"></a>在本节中


-   [INF 文件平台扩展和基于 x64 的系统](inf-file-platform-extensions-and-x64-based-systems.md)
-   [INF 文件平台扩展和基于 x86 的系统](inf-file-platform-extensions-and-x86-based-systems.md)
-   [跨平台 INF 文件](cross-platform-inf-files.md)
-   [将平台扩展与其他节名称扩展相结合](combining-platform-extensions-with-other-section-name-extensions.md)

有关如何使用 INF 文件平台扩展来支持跨平台安装的示例，请参阅 [跨平台 INF 文件](cross-platform-inf-files.md)。

有关如何结合使用平台扩展与节名称扩展的信息，请参阅将 [平台扩展与其他节名称扩展结合](combining-platform-extensions-with-other-section-name-extensions.md)使用。

有关如何通过平台扩展指定目标操作系统的信息，请参阅将 [平台扩展与操作系统版本结合使用](combining-platform-extensions-with-operating-system-versions.md)。

有关可用于在多个操作系统版本中安装驱动程序的示例 INF 文件的信息，请参阅 [在多个版本的 Windows 上安装设备的示例 Inf 文件](sample-inf-file-for-device-installation-on-multiple-versions-of-windows.md)。

 

