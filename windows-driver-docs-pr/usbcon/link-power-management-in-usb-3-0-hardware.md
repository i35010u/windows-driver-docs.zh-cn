---
Description: 本部分提供有关特定限制的通用串行总线 (USB) 2.0 选择性挂起机制的信息。
title: USB 3.0 硬件中的链接电源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7ebed184bf051149d64d0348b70275592014643
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364831"
---
# <a name="link-power-management-in-usb-30-hardware"></a>USB 3.0 硬件中的链接电源管理


本部分提供有关特定限制的通用串行总线 (USB) 2.0 选择性挂起机制的信息。 它为独立硬件供应商 (Ihv) 和原始设备制造商 (Oem) 与选择性挂起结合使用链接电源管理 (LPM) 实现 USB 设备的电源管理提供指南。 它还提供有关 USB 控制器、 中心和设备中的 LPM 实现中的常见缺陷的信息。 此信息适用于 Windows 8 和更高版本。

本部分假定读者熟悉以下内容：

-   官方[USB 3.0 规范](https://www.usb.org/documents)。
-   [USB 选择性挂起](https://go.microsoft.com/fwlink/p/?linkid=230964)机制。 在博客文章介绍机制[揭开面纱 USB 选择性挂起](https://go.microsoft.com/fwlink/p/?linkid=230962)。

## <a name="in-this-section"></a>本节内容


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
<td><p><a href="limitations-of-usb-2-0-mechanism.md" data-raw-source="[Limitations of USB 2.0 Mechanism](limitations-of-usb-2-0-mechanism.md)">USB 2.0 端口的限制机制</a></p></td>
<td><p>介绍通用串行总线 (USB) 2.0 选择性挂起机制的限制。 然后，它提供 USB 3.0 链接电源管理 (LPM) 功能和如何它可以在一起的选择性挂起机制以减少系统功耗的概述。 最后，它列出了在 LPM USB 控制器、 中心和设备中实现常见的缺陷。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-3-0-lpm-mechanism-.md" data-raw-source="[USB 3.0 LPM Mechanism](usb-3-0-lpm-mechanism-.md)">USB 3.0 LPM 机制</a></p></td>
<td><p>本主题介绍的 USB 3.0 LPM 机制。</p>
<p>没有正式的附录<a href="https://go.microsoft.com/fwlink/p/?linkid=230961" data-raw-source="[USB 2.0 Specification](https://go.microsoft.com/fwlink/p/?linkid=230961)">USB 2.0 规范</a>(USB2_LinkPowerMangement_ECN)，其中的较新的 USB 2.0 硬件定义 LPM。 本主题不涉及该 USB 2.0 LPM 机制。 本主题旨在说明 USB 3.0 LPM 状态，尤其是 U1 和 U2。</p></td>
</tr>
<tr class="odd">
<td><p><a href="u1-and-u2-transitions.md" data-raw-source="[U1 and U2 Transitions](u1-and-u2-transitions.md)">U1 和 U2 转换</a></p></td>
<td><p>本主题首先介绍的通过软件来启用 U1 和 U2 转换，并介绍如何在硬件发生这些转换的初始设置。</p></td>
</tr>
<tr class="even">
<td><p><a href="common-hardware-problems-with-u1-or-u2-implementation.md" data-raw-source="[Common Hardware Problems with U1 or U2 Implementation](common-hardware-problems-with-u1-or-u2-implementation.md)">与 U1 或 U2 实现常见的硬件问题</a></p></td>
<td><p>本主题讨论用于保存 power LPM 机制，并介绍各种常见的问题当前 USB 3.0 硬件中所示。 USB-如果认证要求的设备、 集线器和控制器实现 U1 和 U2 正确。 证书的目的是通过符合性测试中强制实施该要求。 Microsoft USB 驱动程序堆栈 （包含在 Windows 8） 充分利用的 U1 和 U2 机制，以实现最大电源节省量。 因此将更频繁地看到问题，例如本主题中所述。 这些问题可能会导致用户体验不佳，并且可能会阻止 Windows 实现提供的 USB 3.0 规范的节能。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[针对 Windows 构建的 USB 设备](building-usb-devices-for-windows.md)  



