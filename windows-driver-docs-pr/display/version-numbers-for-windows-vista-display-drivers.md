---
title: WDDM 驱动程序的版本号
description: WDDM 驱动程序的版本号
ms.assetid: 14608626-cd01-4756-8329-187153a8b99a
keywords:
- 显示驱动程序模型 WDK Windows Vista 中，版本号
- Windows Vista 显示器驱动程序模型 WDK 版本号
- 版本号 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 658900f0a2614e096a854bac49d0871ed5bb1bc9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390780"
---
# <a name="version-numbers-for-wddm-drivers"></a>WDDM 驱动程序的版本号


若要确保符合到 Windows 显示驱动程序模型 (WDDM) 的显示驱动程序或[Windows 2000 显示器驱动程序模型 (XDDM)](windows-2000-display-driver-model-design-guide.md)特定版本的 Microsoft DirectX 使用 Microsoft Windows 上运行，你必须应用对该驱动程序的相应版本号。 如果供应商将显示器驱动程序分发具有错误版本号或使用格式不正确的版本号，最终用户将在安装任何 DirectX 应用程序时遇到困难。

**请注意**   **DriverVer**指令提供了一种方法，若要添加的驱动程序包，其中包括驱动程序文件和 INF 文件本身，到 INF 文件版本信息。 通过使用**DriverVer**指令，您可以安全地和明确替换驱动程序包由同一个包的未来版本。 有关此指令的详细信息，请参阅[ **INF DriverVer 指令**](https://msdn.microsoft.com/library/windows/hardware/ff547394)。

 

此表提供了适用于符合 WDDM 与各种版本的 DirectX 的兼容性的供应商提供的显示器驱动程序的版本号的范围的示例。 \\

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">目标系统</th>
<th align="left">版本号的范围</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WDDM 和 DirectX 9.0 兼容显示驱动程序</p></td>
<td align="left"><p>7.14.01.0000 - 7.14.99.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>WDDM 和 DirectX 10.0 兼容显示驱动程序</p></td>
<td align="left"><p>7.15.01.0000 - 7.15.99.9999</p></td>
</tr>
</tbody>
</table>

 

此表提供的适用于符合的供应商提供的显示器驱动程序的版本编号范围[Windows 2000 显示器驱动程序模型](windows-2000-display-driver-model-design-guide.md)与 DirectX 9.0 的兼容性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">目标系统</th>
<th align="left">版本号的范围</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>XDDM 和 DirectX 9.0 兼容显示驱动程序</p></td>
<td align="left"><p>6.14.01.0000 - 6.14.99.9999</p></td>
</tr>
</tbody>
</table>

 

有关显示器驱动程序的版本控制的详细信息，请参阅[显示驱动程序的版本号](version-numbers-for-display-drivers.md)并[驱动程序版本控制](wddm-2-1-features.md#driver-versioning)。

 

 





