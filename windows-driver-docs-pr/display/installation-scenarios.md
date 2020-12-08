---
title: WDDM 1.2 安装方案
description: Windows 8 安装图形驱动程序的行为旨在确保在可能的情况下，我们的客户获得经过 Windows 8 测试和认证的图形驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2dd793e1b61c951b1f1be034ddd83c2f74bb772
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827231"
---
# <a name="wddm-12-installation-scenarios"></a>WDDM 1.2 安装方案


Windows 8 安装图形驱动程序的行为旨在确保在可能的情况下，我们的客户获得经过 Windows 8 测试和认证的图形驱动程序。 此行为由本部分中描述的规则定义。

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
<td align="left"><p><a href="windows-8-in-box-graphics-driver-preferred-.md" data-raw-source="[Windows 8 in-box graphics driver preferred](windows-8-in-box-graphics-driver-preferred-.md)">首选的 Windows 8 现成图形驱动程序</a></p></td>
<td align="left"><p>在此方案中，Windows 7 或更早版本的图形驱动程序优先于 Windows 8 内置图形驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="windows-8-in-box-graphics-drivers-treated-as-generic-drivers-.md" data-raw-source="[Windows 8 in-box graphics drivers treated as generic drivers](windows-8-in-box-graphics-drivers-treated-as-generic-drivers-.md)">将 Windows 8 现成图形驱动程序视为通用驱动程序</a></p></td>
<td align="left"><p>在此方案中，Windows 8 内置图形驱动程序（包括 MS 基本显示器驱动程序 (MSBDD) ）都被视为 Windows 和 Windows 更新的通用驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wddm-graphics-driver-migrated-to-windows-8.md" data-raw-source="[WDDM graphics driver migrated to Windows 8](wddm-graphics-driver-migrated-to-windows-8.md)">将 WDDM 图形驱动程序迁移到 Windows 8</a></p></td>
<td align="left"><p>如果 Windows 8 升级安装中没有用于图形硬件的窗口8内置范围，则以前版本的 Windows 使用的 WDDM 1.1 或 WDDM 1.0 图形驱动程序将迁移到 Windows 8。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="xddm-drivers--not-supported-for-windows-8-.md" data-raw-source="[XDDM drivers not supported for Windows 8](xddm-drivers--not-supported-for-windows-8-.md)">Windows 8 不支持 XDDM 驱动程序</a></p></td>
<td align="left"><p>Windows 8 不支持 XDDM 驱动程序，并且不会在 Windows 8 上安装或运行。</p></td>
</tr>
</tbody>
</table>

 

 

 





