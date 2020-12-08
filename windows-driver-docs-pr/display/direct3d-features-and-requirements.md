---
title: WDDM 1.2 中的 Direct3D 功能和要求
description: Microsoft Direct3D 提供一系列丰富的3-d 图形 Api，软件应用程序广泛使用这些 Api 来实现复杂的可视化和游戏开发。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e91e300a65b41aaaffe56f25e4363d7a52146ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809471"
---
# <a name="direct3d-features-and-requirements-in-wddm-12"></a>WDDM 1.2 中的 Direct3D 功能和要求


Microsoft Direct3D 提供一系列丰富的3-d 图形 Api，软件应用程序广泛使用这些 Api 来实现复杂的可视化和游戏开发。 本部分介绍功能改进以及 Windows 8 Direct3D 软件和硬件要求。

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
<td align="left"><p><a href="directx-feature-improvements-in-windows-8.md" data-raw-source="[DirectX feature improvements in Windows 8](directx-feature-improvements-in-windows-8.md)">Windows 8 中的 DirectX 功能改进</a></p></td>
<td align="left"><p>Windows 8 包含 Microsoft DirectX 功能改进，可让开发人员、最终用户和系统制造商受益。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="software-requirements.md" data-raw-source="[Direct3D software requirements in Windows 8](software-requirements.md)">Windows 8 中的 Direct3D 软件要求</a></p></td>
<td align="left"><p>本主题介绍在 Windows 8 中支持 Direct3D 的软件要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="hardware-requirements.md" data-raw-source="[Hardware requirements](hardware-requirements.md)">硬件要求</a></p></td>
<td align="left"><p>本主题介绍在 Windows 8 中支持 Direct3D 的硬件要求。</p></td>
</tr>
</tbody>
</table>

 

根据图形适配器的功能，Direct3D 允许应用程序使用整个三维呈现管道或部分加速的硬件加速。 更新版本的 Direct3D Api （如 Direct3D 9Ex 和 Microsoft Direct3D 10）仅适用于 Windows Vista，因为 Windows 显示器驱动程序模型 (WDDM) 提供该功能所需的显示驱动程序接口。 此图显示了在各种版本的 WDDM 上支持的 Direct3D Api 的增量版本：

![各种版本的 wddm 上支持 direct3d api](images/direct3dapissupportedwddm.jpg)

**在各种版本的 WDDM 上支持 Direct3D Api**

 

 





