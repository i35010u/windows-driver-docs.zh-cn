---
title: Direct3D 功能和 WDDM 1.2 中的要求
description: Microsoft Direct3D 提供了一系列丰富的 3-D 图形 Api，广泛使用的软件应用程序以进行复杂的可视化和游戏开发。
ms.assetid: 8A40276D-FAE3-4433-A3E5-573700331B07
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32befb6229afe1856f6dad3c66db68867b29f796
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555909"
---
# <a name="direct3d-features-and-requirements-in-wddm-12"></a>Direct3D 功能和 WDDM 1.2 中的要求


Microsoft Direct3D 提供了一系列丰富的 3-D 图形 Api，广泛使用的软件应用程序以进行复杂的可视化和游戏开发。 本部分介绍功能改进和 Windows 8 Direct3D 软件和硬件要求。

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
<td align="left"><p><a href="directx-feature-improvements-in-windows-8.md" data-raw-source="[DirectX feature improvements in Windows 8](directx-feature-improvements-in-windows-8.md)">在 Windows 8 中的 DirectX 功能改进</a></p></td>
<td align="left"><p>Windows 8 包含 Microsoft DirectX 功能改进，开发人员、 最终用户和系统制造商中受益。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="software-requirements.md" data-raw-source="[Direct3D software requirements in Windows 8](software-requirements.md)">在 Windows 8 中的 Direct3D 软件要求</a></p></td>
<td align="left"><p>本主题介绍在 Windows 8 中支持 Direct3D 的软件要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="hardware-requirements.md" data-raw-source="[Hardware requirements](hardware-requirements.md)">硬件要求</a></p></td>
<td align="left"><p>本主题介绍在 Windows 8 中支持 Direct3D 的硬件要求。</p></td>
</tr>
</tbody>
</table>

 

具体取决于图形适配器的功能，Direct3D 允许应用程序利用硬件加速整个三维呈现管道或部分加速。 例如 Direct3D 9Ex 的 Direct3D Api 和 Microsoft Direct3D 10 的较新版本可仅因为 Windows 显示驱动程序模型 (WDDM) 提供了所需的功能的显示驱动程序接口与 Windows Vista 一起启动。 此图显示了支持 WDDM 的各种版本的 Direct3D Api 的增量版本：

![支持 wddm 的各种版本的 direct3d api](images/direct3dapissupportedwddm.jpg)

**WDDM 的各个版本支持的 Direct3D Api**

 

 





