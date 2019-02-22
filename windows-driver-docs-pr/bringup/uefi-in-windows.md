---
title: Windows 中的 UEFI
description: Windows 中的 UEFI
ms.assetid: 14b54fe3-49f7-4ad8-b9b6-ecc747dff137
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73ce63723ac4fa81625b634647792edc18062b5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533983"
---
# <a name="uefi-in-windows"></a>Windows 中的 UEFI


**请注意**  本部分中的某些信息可能仅适用于 Windows 10 移动版和某些处理器体系结构。

 

Windows 利用统一可扩展固件接口 (UEFI) 以支持从 SoC 固件启动加载程序对操作系统的系统控件的切换。 UEFI 环境是最小的引导时启动的 Windows 设备的 OS 和运行。

UEFI 是基于标准的 UEFI 规范，其中描述了一个标准环境和一组接口以便允许操作系统引导平台固件的引导加载程序的一般框架。 UEFI 规范位于[ http://uefi.org/specifications ](https://go.microsoft.com/fwlink/p/?LinkId=218221)。 由于 UEFI 的极低级别特性，每个其实现是特定于特定 SoC. 适用于 Windows 设备 SoC 供应商提供的核心 UEFI 环境和某些 UEFI 驱动程序。 由 Microsoft 提供了其他 UEFI 驱动程序和 UEFI 应用程序 （例如闪烁的应用程序）。

除了 UEFI 规范中所述的实现详细信息，还有一组额外的 SoC 平台上运行 Windows 的 UEFI 要求。 有关这些要求，请参阅[SoC 平台上的 Windows 最小值 UEFI 要求](minimum-uefi-requirements-for-windows-on-soc-platforms.md)。

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
<td><p><a href="minimum-uefi-requirements-for-windows-on-soc-platforms.md" data-raw-source="[Minimum UEFI requirements for Windows on SoC platforms](minimum-uefi-requirements-for-windows-on-soc-platforms.md)">最小的 Windows 在 SoC 平台上的 UEFI 要求</a></p></td>
<td><p>统一可扩展固件接口 (UEFI) 是用于运行 Windows 的 SoC 平台所需的启动固件。 本部分介绍在 SoC 平台上运行 Windows 的 UEFI 实现需求。 观察并遵循这些要求将有助于确保适当的 Windows 的功能。</p></td>
</tr>
<tr class="even">
<td><p><a href="uefi-protocols-for-windows.md" data-raw-source="[UEFI protocols for Windows](uefi-protocols-for-windows.md)">Windows 的 UEFI 协议</a></p></td>
<td><p>本部分介绍了由 Windows 定义的 UEFI 协议。 这些协议扩展了 UEFI 规范所定义的协议和它们由 Windows 在启动过程中完成特定的函数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="windows-uefi-firmware-update-platform.md" data-raw-source="[Windows UEFI firmware update platform](windows-uefi-firmware-update-platform.md)">Windows UEFI 固件更新平台</a></p></td>
<td><p>Windows 支持一个平台，用于安装系统和通过使用 UEFI UpdateCapsule 函数处理的驱动程序包的设备固件更新。 此平台提供一致、 可靠的固件更新体验，并改进了重要的系统固件更新为最终用户的可发现性。</p></td>
</tr>
</tbody>
</table>

 

## <a name="uefi-components-for-windows"></a>Windows 的 UEFI 组件


下图显示了 Windows 设备的主要 UEFI 组件

![适用于 windows phone 的 uefi 组件](images/oem-uefi-components.png)

## <a name="oem-components-in-the-uefi-environment"></a>UEFI 环境中的 OEM 组件


Oem 可以在制造和服务设备中添加 UEFI 应用程序的帮助。 这些应用程序不应给最终用户访问。 最终用户面向 UEFI 应用程序仅由 Microsoft 实现，由 Windows 启动管理器启动。

Oem 选择实现 UEFI 应用程序应确保它们具有尽可能的内存需求量的一个较小且不会影响启动时间。 有关 UEFI 环境创作组件的详细信息，请咨询 SoC 供应商。

**重要**   Oem 也可能需要更换 SoC 供应商，以匹配其特定的硬件提供的某些 UEFI 驱动程序。 有关详细信息，跟进 SoC 供应商。

 

## <a name="related-topics"></a>相关主题
[Windows 的 UEFI 协议](uefi-protocols-for-windows.md)  



