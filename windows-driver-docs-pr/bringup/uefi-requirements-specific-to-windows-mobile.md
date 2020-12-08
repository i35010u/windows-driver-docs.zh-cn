---
title: Windows 10 移动版的 UEFI 要求
description: 除了适用于所有 Windows 版本的 UEFI 要求以外，Windows 10 移动版设备必须满足本主题中所述的其他要求。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfe3f3464d65dfac49f5e4c14c1dbb2ed2578846
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787059"
---
# <a name="uefi-requirements-for-windows-10-mobile"></a>Windows 10 移动版的 UEFI 要求


除了 [适用于所有 Windows 版本的 uefi 要求](uefi-requirements-that-apply-to-all-windows-platforms.md)中列出的 uefi 要求之外，运行 Windows 10 移动版的设备还必须满足本主题中所述的其他要求。

## <a name="requirements-that-expand-on-the-general-uefi-requirements-for-all-windows-editions"></a>对所有 Windows 版本的常规 UEFI 要求进行扩展的要求


下表描述了 Windows 10 移动版的 UEFI 要求，该要求扩展了适用于 [所有 Windows 版本的 uefi 要求](uefi-requirements-that-apply-to-all-windows-platforms.md)中所述的要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要求</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>GPT</td>
<td>设备必须能够从 GUID 分区表启动 (GPT) 。 此外，设备必须包括主 GPT 和备用 GPT，如 UEFI 规范的 "GUID 分区表磁盘布局" 5.3 一节中所述。</td>
</tr>
<tr class="even">
<td>变量服务</td>
<td>变量服务至少必须提供 64 KB 的非易失性存储空间，以供 Microsoft 使用。 此外，必须在标记的存储位置中实现这些变量服务。 需要有足够的空间来存储密钥和其他参数以进行安全启动，这样，就可以用新的变量来闪烁整个存储，并在闪烁整个存储时允许排除这些变量。 为了降低 BOM 成本和硬件复杂性，Microsoft 要求不要通过向设备添加额外的闪存部件来实现可变服务。</td>
</tr>
<tr class="odd">
<td>简单文本输入协议</td>
<td><p>以下物理键应映射到以下函数：</p>
<ul>
<li>调高音量：向上键</li>
<li>调高音量：向下箭头</li>
<li>照相机：输入</li>
<li>电源按钮：挂起</li>
</ul></td>
</tr>
<tr class="even">
<td>内存服务</td>
<td>GetMemoryMap ( # A1 函数必须返回该平台的所有物理内存，如 UEFI 规范的6.2 节 "内存服务" 中所述。</td>
</tr>
<tr class="odd">
<td>EFI 块 i/o 协议</td>
<td>EFI 块 i/o 协议必须根据其本机扇区大小报告存储设备大小。 例如，4 KB 扇区设备不应将自身报告为512字节扇区设备。</td>
</tr>
</tbody>
</table>



## <a name="requirements-specific-to-windows-10-mobile"></a>特定于 Windows 10 移动版的要求


下表描述了特定于 Windows 10 移动版的要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要求</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UEFI 驱动程序</td>
<td>UEFI 驱动程序必须嵌入 UEFI 固件。</td>
</tr>
<tr class="even">
<td>USB 函数协议</td>
<td>UEFI 固件必须包含符合 UEFI USB function 协议的驱动程序。 有关详细信息，请参阅 <a href="uefi-usb-function-protocol.md" data-raw-source="[UEFI USB function protocol](uefi-usb-function-protocol.md)">UEFI USB 函数协议</a>。 UEFI 中的 USB 枚举仅应由 Microsoft 代码处理。</td>
</tr>
<tr class="odd">
<td>电池充电协议</td>
<td><p>如果设备使用 Microsoft UEFI 电池充电应用程序，则 UEFI 固件必须包含实现 UEFI 电池充电协议的驱动程序。 在设备移交给 Microsoft UEFI 电池充电软件之前，设备必须符合 <em>USB 电池充电版本1.2 规范</em>。 有关详细信息，请参阅<a href="battery-charging-in-the-boot-environment.md" data-raw-source="[Battery charging in the boot environment](battery-charging-in-the-boot-environment.md)">启动环境中的</a> <a href="uefi-battery-charging-protocol.md" data-raw-source="[UEFI battery charging protocol](uefi-battery-charging-protocol.md)">UEFI 电池充电协议</a>和电池充电。</p>
<div class="alert">
<strong>重要提示</strong>  仅当设备使用 Microsoft UEFI 电池充电应用程序时，此要求才适用。 如果设备使用自定义的 UEFI 电池充电应用程序而不是 Microsoft 提供的应用程序，则 UEFI 电池充电驱动程序不得实现 UEFI 电池充电协议。
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td>显示电源状态协议</td>
<td><p>如果设备使用 Microsoft UEFI 电池充电应用程序，则 UEFI 固件必须包含实现 UEFI 显示电源状态协议的驱动程序。 此协议用于在 UEFI 环境中充电时关闭屏幕，并将其关闭并重新打开。 有关此协议的详细信息，请参阅 <a href="uefi-display-power-state-protocol.md" data-raw-source="[UEFI display power state protocol](uefi-display-power-state-protocol.md)">UEFI 显示电源状态协议</a>。 有关 UEFI 电池充电应用程序如何使用此协议的详细信息，请参阅 <a href="architecture-of-the-uefi-battery-charging-application.md" data-raw-source="[Architecture of the UEFI battery charging application](architecture-of-the-uefi-battery-charging-application.md)">uefi 电池充电应用程序的体系结构</a>。</p>
<div class="alert">
<strong>重要提示</strong>  仅当设备使用 Microsoft UEFI 电池充电应用程序时，此要求才适用。 如果设备使用自定义的 UEFI 电池充电应用程序而不是 Microsoft 提供的应用程序，则 UEFI 电池充电驱动程序不得实现 UEFI 显示电源状态协议。
</div>
<div>

</div></td>
</tr>
<tr class="odd">
<td>电源优化</td>
<td>建议将 UEFI 环境优化为不使用过多的电源。 这允许设备在启动时尽可能少地使用电源，并在 UEFI) 中充电时尽快 (。</td>
</tr>
<tr class="even">
<td>保留硬件按钮</td>
<td><p>在启动过程中，Microsoft 定义独立的电源、调高和调低音量按钮作为可用于启动多个 Microsoft 提供的 UEFI 应用程序的触发器。 在启动过程中，Oem 不得重载 power、volume up 或 volume down 按钮来执行自定义操作或启动其他 UEFI 应用程序。</p>
<p>以下列表显示了由这些按钮启动的 Microsoft 提供的 UEFI 应用程序。</p>
<ul>
<li>增加容量： Microsoft 提供的 UEFI 闪烁应用程序。</li>
<li>缩小： Microsoft 提供的 UEFI 设备重置应用程序。</li>
<li>Power： Microsoft 提供的开发人员启动菜单应用程序。</li>
</ul>
<div class="alert">
<strong>注意</strong><br/><p>Oem 还必须确保在 UEFI 环境中将 "音量调高" 和 "音量减小" 按钮分别充当向上箭头键和向下箭头键。</p>
</div>
<div>

</div></td>
</tr>
<tr class="odd">
<td>OEM UEFI 应用程序</td>
<td><p>Oem 可以添加 UEFI 应用程序来帮助制造和服务设备。 这些应用程序具有以下限制：</p>
<ul>
<li><p>UEFI 应用程序不应影响启动时间。</p></li>
<li><p>UEFI 应用程序必须使用允许的签名数据库 (db) UEFI 变量中的证书进行签名。</p></li>
<li><p>UEFI 应用程序必须采用以下方法之一：</p>
<ul>
<li><p>它们 <em>永远不</em> 能在启动到主操作系统或更新操作系统的过程中运行。</p>
<p>\- 或 -</p></li>
<li><p>它们必须 <em>始终</em> 在启动到主操作系统或更新操作系统的过程中运行。</p></li>
</ul></li>
</ul>
<p>UEFI 应用程序有时 <em>不</em> 能运行，有时不能在启动到主操作系统或更新 os 的过程中运行。 启用设备加密后，受信任的平台模块 (TPM) 存储启动顺序，并且在启用设备加密后，不能对其进行更改。 例如，如果启动序列是 <em>UEFI 固件</em> &gt; <em>应用程序 a</em> &gt; bootarm，则从启动序列中删除 <em>应用程序 a</em> 将导致 TPM 无法解封。</p>
<p>此外，如果有多个 UEFI 应用程序，固件应确保应用程序的顺序一致。 例如，如果启动序列是<em>UEFI 固件</em> &gt; <em>应用</em> &gt; <em>程序 a 应用程序 b</em> &gt; bootarm，则在应用<em>UEFI firmware</em> &gt; <em>application B</em> &gt; 程序 a 和 B 链接到数据库中的不同项时，将启动顺序更改为 uefi 固件应用程序 b<em>应用程序 a</em> &gt; bootarm 可能导致 TPM 无法解封。</p>
<p>更新启动应用程序的签名证书不会导致 TPM 问题。 但是，如果 UEFI 应用程序重新签名，使其链接到 db 中的其他条目，则这也会导致 TPM 无法解封。</p></td>
</tr>
</tbody>
</table>



## <a name="related-topics"></a>相关主题
[SoC 平台上的 Windows 的最低 UEFI 要求](minimum-uefi-requirements-for-windows-on-soc-platforms.md)  
[适用于所有 Windows 版本的 UEFI 要求](uefi-requirements-that-apply-to-all-windows-platforms.md)  
[USB 刷写支持的 UEFI 要求](uefi-requirements-for-usb-flashing-support.md)  



