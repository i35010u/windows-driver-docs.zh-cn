---
title: 创建适用于多个平台和操作系统的 INF 文件
description: 创建适用于多个平台和操作系统的 INF 文件
ms.assetid: 61996c72-c5a7-4ff0-aeb3-6e77b77542c8
keywords:
- INF 文件 WDK 设备安装多个平台和操作系统
- 多个操作系统 WDK、 INF 文件
- 跨平台 INF 文件 WDK
- 操作系统 WDK，跨操作系统系统 INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2e1eea87b4be2374b764981dcc7288e94ae469a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381502"
---
# <a name="creating-inf-files-for-multiple-platforms-and-operating-systems"></a>创建适用于多个平台和操作系统的 INF 文件





通过使用系统定义的平台扩展[INF 文件的部分和指令](inf-file-sections-and-directives.md)，可以创建跨平台安装的单个 INF 文件。 扩展，您可以创建*修饰*部分名称，指定与每个目标平台和操作系统相关的部分和指令。 例如，可以创建仅在基于 x64 的系统上，仅在基于 Itanium 的系统上，仅在基于 x86 的系统上或在 Windows 2000 和更高版本的 Windows 支持的所有系统上安装设备的 INF 文件。

下表总结了可以添加到的部分支持扩展的名称的系统支持的平台扩展。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">平台扩展</th>
<th align="left">将</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>.ntamd64</strong></p></td>
<td align="left"><p>部分包含有关由 Windows XP 及更高版本支持的基于 x64 的系统上安装一个设备或一组兼容设备的模型的说明。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.ntia64</strong></p></td>
<td align="left"><p>部分包含有关由 Windows XP 及更高版本支持的基于 Itanium 的系统上安装一个设备或一组兼容设备的模型的说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>.ntx86</strong></p></td>
<td align="left"><p>部分包含有关由 Windows XP 及更高版本支持的基于 x86 的系统上安装一个设备或一组兼容设备的模型的说明。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.ntarm</strong></p></td>
<td align="left"><p>部分包含有关通过 Windows 8 及更高版本支持的基于 ARM 的系统上安装一个设备或一组兼容设备的模型的说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>.ntarm64</strong></p></td>
<td align="left"><p>部分包含有关支持的 Windows 10 版本 1709年及更高版本的基于 ARM64 的系统上安装一个设备或一组兼容设备的模型的说明。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.nt</strong></p></td>
<td align="left"><p>在 Windows 的以前版本 Windows Server 2003 SP1，部分包含所有支持的操作系统的系统上安装一个设备或一组兼容设备的模型的说明。</p>
<p>从 Windows Server 2003 SP1 开始，部分包含有关支持的操作系统的基于 x86 的系统上安装一个设备或一组兼容设备的模型的说明。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>（无扩展名平台）</p></td>
<td align="left"><p>在 Windows 的以前版本 Windows Server 2003 SP1，部分包含所有支持的操作系统的系统上安装一个设备或一组兼容设备的模型的说明。</p>
<p>从 Windows Server 2003 SP1 开始，部分包含有关支持的操作系统的基于 x86 的系统上安装一个设备或一组兼容设备的模型的说明。</p></td>
</tr>
</tbody>
</table>

 

**重要**  从 Windows Server 2003 SP1 开始，INF 文件必须修饰中的条目[ **INF 模型部分**](inf-models-section.md)与。**ntia64**，。**ntarm**，。**ntarm64**或。**ntamd64**平台扩展，以指定非 x86 目标操作系统版本。 对于基于 x86 的目标操作系统版本的 INF 文件或非 PnP 驱动程序 INF 文件 （例如基于 x64 的体系结构的文件系统驱动程序 INF 文件） 中不需要这些平台扩展。

 

**提示**我们强烈建议您始终修饰中的条目[ **INF 模型部分**](inf-models-section.md)以及目标出的 Windows XP 和更高版本的 Windows 的平台扩展。 对于基于 x86 的硬件平台，应避免使用 **.nt**平台扩展，并使用 **.ntx86**相反。

 

## <a name="in-this-section"></a>本节内容


-   [INF 文件平台扩展和基于 x64 的系统](inf-file-platform-extensions-and-x64-based-systems.md)
-   [INF 文件平台扩展和基于 x86 的系统](inf-file-platform-extensions-and-x86-based-systems.md)
-   [跨平台 INF 文件](cross-platform-inf-files.md)
-   [结合与其他部分名称扩展的平台扩展](combining-platform-extensions-with-other-section-name-extensions.md)

有关如何使用 INF 文件平台扩展来支持跨平台安装的示例，请参阅[跨平台 INF 文件](cross-platform-inf-files.md)。

有关如何使用在部分名称扩展结合使用的平台扩展的信息，请参阅[组合平台扩展与其他部分名称扩展](combining-platform-extensions-with-other-section-name-extensions.md)。

有关如何指定通过平台扩展的目标操作系统的信息，请参阅[结合使用的操作系统版本的平台扩展](combining-platform-extensions-with-operating-system-versions.md)。

有关可用于在多个操作系统版本中安装驱动程序的示例 INF 文件的信息，请参阅[上多个版本的 Windows 设备安装的示例 INF 文件](sample-inf-file-for-device-installation-on-multiple-versions-of-windows.md)。

 

 





