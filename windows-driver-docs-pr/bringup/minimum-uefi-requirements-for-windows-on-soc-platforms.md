---
title: 最小的 Windows 在 SoC 平台上的 UEFI 要求
description: 最小的 Windows 在 SoC 平台上的 UEFI 要求
ms.assetid: 32743d69-83a2-4658-8652-6d624e75e3db
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cfb1408e1c2d1a19cb9bd0fd2bc25dd22821568
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525655"
---
# <a name="minimum-uefi-requirements-for-windows-on-soc-platforms"></a>最小的 Windows 在 SoC 平台上的 UEFI 要求


统一可扩展固件接口 (UEFI) 是用于运行 Windows 的 SoC 平台所需的启动固件。 本部分介绍在 SoC 平台上运行 Windows 的 UEFI 实现需求。 观察并遵循这些要求将有助于确保适当的 Windows 的功能。

这组需求适用于任何基于 SoC 的计算系统中，有一些限制。 本指南假定完整的 Windows 功能集，支持传统的上网本的外观造型和无线、 仅限多点触控的移动设备。 因此限制本身为应在此类系统中广泛使用的技术。 对于未涵盖的技术实施本文档中的系统，请参阅在 UEFI 规范[UEFI 规范](https://go.microsoft.com/fwlink/p/?LinkId=218221)。

Windows 支持基于统一可扩展固件接口 (UEFI) 版本 2.3.1 或更高版本的固件版本。

**请注意**  Windows 支持 UEFI 2.3.1 中定义的功能的子集规范。 Windows 实现不具有显式签入被更高版本的固件修订。 如果它们包含必要的支持本文档中所述，操作系统将支持更高版本的修订版本的固件。

 

## <a name="in-this-section"></a>本部分内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="uefi-requirements-that-apply-to-all-windows-platforms.md" data-raw-source="[UEFI requirements that apply to all Windows editions on SoC platforms](uefi-requirements-that-apply-to-all-windows-platforms.md)">适用于 SoC 平台上的所有 Windows 版本的 UEFI 要求</a></p></td>
<td><p>本主题介绍适用于 Windows 10 桌面版 （主页、 专业版、 企业版和教育版） 和 Windows 10 移动版的 UEFI 要求。</p></td>
</tr>
<tr class="even">
<td><p><a href="uefi-requirements-specific-to-windows-mobile.md" data-raw-source="[UEFI requirements for Windows 10 Mobile](uefi-requirements-specific-to-windows-mobile.md)">Windows 10 移动版的 UEFI 要求</a></p></td>
<td><p>除了中列出的 UEFI 要求<a href="uefi-requirements-that-apply-to-all-windows-platforms.md" data-raw-source="[UEFI requirements that apply to all Windows editions](uefi-requirements-that-apply-to-all-windows-platforms.md)">适用于所有 Windows 版本的 UEFI 要求</a>，运行 Windows 10 移动版的设备还必须满足本主题中所述的其他要求。</p></td>
</tr>
<tr class="odd">
<td><p><a href="uefi-requirements-for-usb-flashing-support.md" data-raw-source="[UEFI requirements for USB flashing support](uefi-requirements-for-usb-flashing-support.md)">USB 闪烁的支持的 UEFI 要求</a></p></td>
<td><p>Microsoft 提供用于在设计和制造环境中使用多个基于 USB 的闪烁的解决方案。 按顺序，使设备能够与这些工具一起使用，在设备上的 UEFI 环境必须满足本主题中列出的要求。</p></td>
</tr>
</tbody>
</table>

 

 

 




