---
title: Windows 10 移动版的 UEFI 要求
description: 除了适用于所有 Windows 版本的 UEFI 要求，Windows 10 移动版设备必须满足本主题中所述的其他要求。
ms.assetid: 12a03f5b-1717-4daf-90ef-5e530f72b19e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e144aa50e4d664cc5766d9297410afcd8db7f22
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464259"
---
# <a name="uefi-requirements-for-windows-10-mobile"></a>Windows 10 移动版的 UEFI 要求


除了中列出的 UEFI 要求[适用于所有 Windows 版本的 UEFI 要求](uefi-requirements-that-apply-to-all-windows-platforms.md)，运行 Windows 10 移动版的设备还必须满足本主题中所述的其他要求。

## <a name="requirements-that-expand-on-the-general-uefi-requirements-for-all-windows-editions"></a>展开的常规的 UEFI 要求的所有 Windows 版本的要求


下表介绍了进一步扩展前面的这些要求中所述的 UEFI 要求适用于 Windows 10 移动设备[适用于所有 Windows 版本的 UEFI 要求](uefi-requirements-that-apply-to-all-windows-platforms.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要求</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>GPT</td>
<td>设备必须能够启动从 GUID 分区表 (GPT)。 此外，设备必须包含这两个主数据库和 5.3 部分中所述的备份 GPT UEFI 规范的标题为"GUID 分区表磁盘布局"。</td>
</tr>
<tr class="even">
<td>变量服务</td>
<td>变量服务必须提供至少 64 KB 的非易失性存储供 Microsoft 使用。 此外，必须在存储的标记位置中实现这些变量服务。 此要求是拥有足够的空间来存储密钥和安全启动，以允许闪烁的整个存储使用新的变量，并允许这些变量的排除时闪烁的整个存储的其他参数。 若要减少 BOM 成本和硬件的复杂性，Microsoft 要求必须通过添加到设备的额外闪存部分实现变量服务。</td>
</tr>
<tr class="odd">
<td>简单的文本输入的协议</td>
<td><p>以下物理密钥应映射到以下函数：</p>
<ul>
<li>调高音量：向上键</li>
<li>调高音量：向下箭头</li>
<li>照相机：Enter</li>
<li>电源按钮：暂停</li>
</ul></td>
</tr>
<tr class="even">
<td>内存服务</td>
<td>GetMemoryMap() 函数必须返回完整的物理内存的平台，即指定的 UEFI 规范的 6.2 节"内存服务"的范围。</td>
</tr>
<tr class="odd">
<td>EFI 块 I/O 协议</td>
<td>EFI 块 I/O 协议必须报告基于其本机扇区大小的存储设备大小。 例如，4 KB 扇区设备应报告本身为 512 字节扇区的设备。</td>
</tr>
</tbody>
</table>



## <a name="requirements-specific-to-windows-10-mobile"></a>特定于 Windows 10 移动版的要求


下表介绍特定于 Windows 10 移动版的要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要求</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UEFI 驱动程序</td>
<td>必须在 UEFI 固件中嵌入 UEFI 驱动程序。</td>
</tr>
<tr class="even">
<td>USB 函数协议</td>
<td>UEFI 固件必须包括符合 UEFI USB 函数协议的驱动程序。 有关详细信息，请参阅<a href="uefi-usb-function-protocol.md" data-raw-source="[UEFI USB function protocol](uefi-usb-function-protocol.md)">UEFI USB 函数协议</a>。 在 UEFI 中的 USB 枚举仅应由 Microsoft 代码处理。</td>
</tr>
<tr class="odd">
<td>电池充电协议</td>
<td><p>如果设备使用 Microsoft UEFI 电池充电应用程序，UEFI 固件必须包括实现 UEFI 电池充电协议的驱动程序。 在设备工作移交给 Microsoft UEFI 电池充电软件之前，设备必须遵从<em>USB 电池充电 v1.2 规范</em>。 有关详细信息，请参阅<a href="uefi-battery-charging-protocol.md" data-raw-source="[UEFI battery charging protocol](uefi-battery-charging-protocol.md)">UEFI 电池充电协议</a>并<a href="battery-charging-in-the-boot-environment.md" data-raw-source="[Battery charging in the boot environment](battery-charging-in-the-boot-environment.md)">启动环境中的电池充电</a>。</p>
<div class="alert">
<strong>重要</strong>此要求仅适用于设备使用 Microsoft UEFI 电池充电应用程序。 如果设备使用的自定义的 UEFI 电池充电应用而不是由 Microsoft 提供的应用程序，UEFI 电池充电驱动程序必须实现 UEFI 电池充电协议。
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td>显示电源状态协议</td>
<td><p>如果设备使用 Microsoft UEFI 电池充电应用程序，UEFI 固件必须包括实现 UEFI 显示电源状态协议的驱动程序。 此协议用于关闭该屏幕和背景光和启用重新充电 UEFI 环境中时。 有关此协议的详细信息，请参阅<a href="uefi-display-power-state-protocol.md" data-raw-source="[UEFI display power state protocol](uefi-display-power-state-protocol.md)">UEFI 显示电源状态协议</a>。 有关 UEFI 电池充电应用程序如何使用此协议的详细信息，请参阅<a href="architecture-of-the-uefi-battery-charging-application.md" data-raw-source="[Architecture of the UEFI battery charging application](architecture-of-the-uefi-battery-charging-application.md)">UEFI 电池充电应用程序的体系结构</a>。</p>
<div class="alert">
<strong>重要</strong>此要求仅适用于设备使用 Microsoft UEFI 电池充电应用程序。 如果设备使用自定义 UEFI 电池充电而不是由 Microsoft 提供的应用程序的应用程序，UEFI 电池充电驱动程序必须不实现 UEFI 显示电源状态协议。
</div>
<div>

</div></td>
</tr>
<tr class="odd">
<td>电源优化</td>
<td>建议 UEFI 环境进行电源优化，以便不使用过量的功率。 这允许设备在要用作启动，同时尽可能少的功率和 （在充电在 UEFI 中） 时尽快从收取相关费用。</td>
</tr>
<tr class="even">
<td>保留的硬件按钮</td>
<td><p>在启动过程中，Microsoft 定义了独立电源、 卷，按下向上和向下按钮一样，将触发卷可用于启动多个由 Microsoft 提供的 UEFI 应用程序。 Oem 必须不能重载 power、 音量增大或减小音量期间执行自定义操作或启动其他 UEFI 应用程序的启动按钮。</p>
<p>以下列表显示哪些 Microsoft 提供的 UEFI 应用程序都已启动这些按钮。</p>
<ul>
<li>调高音量：闪烁的应用程序提供 Microsoft UEFI。</li>
<li>调低音量：Microsoft 提供的 UEFI 设备重置应用程序。</li>
<li>电源：Microsoft 提供的开发人员启动菜单应用程序。</li>
</ul>
<div class="alert">
<strong>注意</strong><br/><p>Oem 必须确保调高音量和调低音量按钮函数按向上键和 UEFI 环境中的分别向下箭头键。</p>
</div>
<div>

</div></td>
</tr>
<tr class="odd">
<td>OEM UEFI 应用程序</td>
<td><p>Oem 可以在制造和服务设备中添加 UEFI 应用程序的帮助。 这些应用程序具有以下限制：</p>
<ul>
<li><p>UEFI 应用程序不应影响启动时间。</p></li>
<li><p>UEFI 应用程序必须使用允许的签名数据库 (db) UEFI 变量中的证书进行签名。</p></li>
<li><p>UEFI 应用程序必须通过以下方式之一中的行为：</p>
<ul>
<li><p>它们必须<em>永远不会</em>主要 OS 在启动期间运行或更新操作系统。</p>
<p>— 或 —</p></li>
<li><p>它们必须<em>始终</em>主要 OS 在启动期间运行或更新操作系统。</p></li>
</ul></li>
</ul>
<p>UEFI 应用程序<em>不得</em>有时运行和有时不到主要 OS 在启动期间运行或更新操作系统。 启用设备加密后，受信任的平台模块 (TPM) 存储的启动顺序，并启用设备加密后，不能更改它。 例如，如果在启动序列为<em>UEFI 固件</em> &gt; <em>应用程序 A</em> &gt; bootarm.efi，然后将其删除<em>应用程序 A</em>启动从序列将导致 TPM 不能通过取消密封。</p>
<p>此外，如果有多个 UEFI 应用程序，应确保固件一致的应用程序的顺序。 例如，如果在启动序列为<em>UEFI 固件</em> &gt; <em>应用程序 A</em> &gt; <em>应用程序 B</em> &gt; bootarm.efi，然后更改到的启动顺序<em>UEFI 固件</em> &gt; <em>应用程序 B</em> &gt; <em>应用程序 A</em> &gt; bootarm.efi可能会导致 TPM 不能通过取消密封如果 A 和 B 的应用程序链接到 db 中的不同项。</p>
<p>正在更新的启动应用程序的签名证书不会导致 TPM 的问题。 但是，如果 UEFI 应用程序重新签名，以便它们链接到 db 中的不同项，然后这还会 TPM 不能通过取消密封。</p></td>
</tr>
</tbody>
</table>



## <a name="related-topics"></a>相关主题
[最小的 Windows 在 SoC 平台上的 UEFI 要求](minimum-uefi-requirements-for-windows-on-soc-platforms.md)  
[适用于所有 Windows 版本的 UEFI 要求](uefi-requirements-that-apply-to-all-windows-platforms.md)  
[USB 闪烁的支持的 UEFI 要求](uefi-requirements-for-usb-flashing-support.md)  



