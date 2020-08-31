---
title: WDDM 驱动程序的版本号
description: WDDM 驱动程序的版本号
ms.assetid: 14608626-cd01-4756-8329-187153a8b99a
keywords:
- 显示驱动程序模型 WDK Windows Vista，版本号
- Windows Vista 显示器驱动程序模型 WDK，版本号
- WDK 显示的版本号
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9f4c5a5beb4b5ee0161e962c9f2186702bebea8
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067018"
---
# <a name="version-numbers-for-wddm-drivers"></a>WDDM 驱动程序的版本号


若要确保符合 Windows 显示驱动程序模型 (WDDM) 或 [windows 2000 显示驱动程序模型 ](windows-2000-display-driver-model-design-guide.md) 的显示驱动程序 (XDDM) 在 microsoft Windows 上使用特定版本的 microsoft DirectX 运行，则必须向该驱动程序应用适当的版本号。 如果供应商分发的显示驱动程序的版本号错误或使用错误格式的版本号，最终用户在安装任何 DirectX 应用程序时将遇到问题。

**注意**   **DriverVer**指令提供一种将驱动程序包的版本信息（包括驱动程序文件和 inf 文件本身）添加到 INF 文件的方法。 使用 **DriverVer** 指令，可安全且最终地替换同一包的未来版本中的驱动程序包。 有关此指令的详细信息，请参阅 [**INF DriverVer 指令**](../install/inf-driverver-directive.md)。

 

此表提供了适用于供应商提供的显示驱动程序的版本号范围的示例，这些驱动程序符合 WDDM 与各种 DirectX 版本的兼容性。 \\

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">目标系统</th>
<th align="left">版本号范围</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WDDM 和 DirectX 9.0 兼容的显示驱动程序</p></td>
<td align="left"><p>7.14.01.0000 - 7.14.99.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>WDDM 和 DirectX 10.0 兼容的显示驱动程序</p></td>
<td align="left"><p>7.15.01.0000 - 7.15.99.9999</p></td>
</tr>
</tbody>
</table>

 

此表提供适用于供应商提供的显示驱动程序的版本号范围，这些驱动程序符合 [Windows 2000 显示器驱动程序模型](windows-2000-display-driver-model-design-guide.md) 与 DirectX 9.0 的兼容性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">目标系统</th>
<th align="left">版本号范围</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>XDDM 和 DirectX 9.0 兼容的显示驱动程序</p></td>
<td align="left"><p>6.14.01.0000 - 6.14.99.9999</p></td>
</tr>
</tbody>
</table>

 

有关显示驱动程序的版本控制的详细信息，请参阅 [显示驱动程序的版本号](version-numbers-for-display-drivers.md) 和 [驱动程序版本控制](wddm-2-1-features.md#driver-versioning)。

 

