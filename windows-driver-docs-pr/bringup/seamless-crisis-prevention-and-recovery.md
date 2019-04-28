---
title: 无缝危机预防和恢复
description: 如果固件更新失败，结果可能极具破坏性。
ms.assetid: F002100E-2505-4CCB-B048-27D9CA1C8F3E
ms.date: 08/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: 16834207ba494d9d5e68b3ecfbdbc7881ac9538d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337394"
---
# <a name="seamless-crisis-prevention-and-recovery"></a>无缝危机预防和恢复


如果固件更新失败，结果可能极具破坏性。 充其量，更新失败，但系统可以灵活，并且恢复而无需最终用户开始了解。 最坏的情形，很可能会导致完全不可用的系统，要求最终用户将他们的系统返回到零售商、 制造商联系以修复失败的固件更新。 后一种情况是我们所说*危机*。

失败的固件更新，或由于与 Windows 或系统的其他方面不兼容的固件，可以导致危机。 本部分讨论功能，旨在预防和恢复从危机的导致的失败的固件更新。 我们预期结果是由固件作者的固件更新测试覆盖范围将阻止大部分危机导致的不兼容的固件。

以便为最终用户提供更完美的体验，必须满足以下危机预防和恢复要求，固件驱动程序程序包更新机制。 这些要求并不排除其他危机保护或恢复解决方案。

## <a name="pre-installation-criteria"></a>预安装条件


执行系统固件的实际更新时，必须执行的安装前检查一系列。 系统固件必须执行此检查，确保足够的电源来完成更新。 此外建议检查次数为每个更新后应用更新后，如果有多个固件更新。 下面提供了检查并验证的项的列表。 在适用的情况，必须执行所有检查。 没有任何特定顺序执行的测试。

<table>
<colgroup>
<col width="20%" />
<col width="80%" />
</colgroup>
<thead>
<tr class="header">
<th>检查类型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>电源</td>
<td><ul>
<li>系统必须具有至少 25%电池电量。</li>
<li>受限的 power （电源通过 USB 电缆） 和/或 AC 电源，则不需要。</li>
</ul>
<div class="alert">
<strong>请注意</strong>  在测试/实验室提供的环境是可以接受的没有电池存在但仍允许固件更新，只要已接入的电源。 但是必须停用/不充电电池与没有电池存在之间进行区分。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td>安全性</td>
<td><ul>
<li>验证更新是否已正确签名封装有效负载。</li>
<li>验证有效负载中的任何基于 PE 的 EFI 文件进行了正确签名使用正确的 EFI 证书。</li>
</ul></td>
</tr>
<tr class="odd">
<td>完整性</td>
<td><p>对执行完整性检查固件更新有效负载。</p></td>
</tr>
<tr class="even">
<td>Version</td>
<td><p>验证正在应用固件不降级 LowestSupportedFirmwareVersion 值超出当前的已安装的固件。</p></td>
</tr>
<tr class="odd">
<td>存储</td>
<td><p>根据需要，根据系统的硬件执行以下检查</p>
<ul>
<li>没有足够空间，以便将取代当前固件的备份</li>
<li>中的设备以适应新的固件没有足够的空间</li>
</ul></td>
</tr>
</tbody>
</table>

 

出现任何故障必须导致相应的上次尝试状态错误代码。 有关详细信息，请参阅中的上一次尝试状态错误代码信息[ESRT 表定义](esrt-table-definition.md)并[固件更新状态](firmware-update-status.md)。

如果应用多个更新和一些通过预安装检查和其他人不这样做，可以继续平台固件更新为使用传递预安装检查的资源的固件。 但是，必须更新安装前检查失败的任何资源。

## <a name="post-installation-criteria"></a>安装后条件

在安装了固件 （设备或系统） 之后必须已检查来验证新的已更新的固件映像已超出预期。 这是为了在实际的更新过程 （例如闪存 rom 期间更新等的总线上的干扰的 sticky 位） 引入了任何损坏任何风险降至最低。

更新过程中必须验证已更新的固件通过完整性检查。 如果它失败，则它必须恢复通过回滚到上次已知的良好的固件版本。

出现任何故障必须导致相应的上次尝试状态错误代码。 有关详细信息，请参阅中的上一次尝试状态错误代码信息[ESRT 表定义](esrt-table-definition.md)并[固件更新状态](firmware-update-status.md)。

## <a name="recovering-from-install-and-boot-failures"></a>从安装和启动故障恢复

为了防止系统不可启动状态，固件更新机制必须满足以下要求在情况下，固件更新无法安装，或在使系统无法成功启动的情况下。

> [!NOTE]
> 在以下部分中，"已提交"术语用于描述固件。 固件"提交"后，固件被视为完全安装，并且将不会自动回滚固件由于启动故障，等等。"未提交的"固件介绍部分已更新的固件，并可以有可能将其回滚到以前的版本中无法完成固件更新或更新固件检测到故障的情况下 (例如，无效的 CRC 签入更新）。 提交固件是否是指固件在内部，应跟踪并不会捕获 ESRT 的一部分。

### <a name="firmware-update-unsuccessful"></a>固件更新失败

如果单个系统或设备固件不能安装或安装了不正确 （例如，由于某种类型的损坏或安装更新时在电源中断），可能最多的尝试三 （3），包括第一个更新会重试尝试。 如果固件会执行其他重试次数，系统必须不会启动到任何尝试之间的 Windows。 如果所有尝试都失败，则更新固件必须丢弃更新。 如果部分应用更新，固件必须将还原到以前的版本。 固件必须回滚到以前的版本，无需任何用户交互。 更新失败不会影响其他挂起的更新;挂起的固件，应尝试更新。

处理完所有更新后，将恢复 UEFI 启动 Windows。 UEFI 固件必须验证任何非提交固件更新已成功安装为了缓解问题由于断电 （UEFI 应永远不会尝试启动 Windows 使用部分编写固件）。

安装失败的可能原因包括但不限于：

-   资源不足
-   在电源中断
-   硬件故障

### <a name="firmware-update-succeeds-but-windows-fails-to-boot"></a>固件更新将成功，但 Windows 无法启动

UEFI 固件不负责后已被提交回滚已更新的固件。 在 Windows 中的现有故障转移逻辑将转移到 Windows 恢复环境 (WinRE) 最终用户后两个不成功启动尝试。 WinRE 可能或可能无法成功启动。 最终用户将需要执行手动恢复步骤，以恢复他们的系统，或必须将其设备恢复至零售商/制造商。

此类故障的可能原因包括但不限于：

-   固件与操作系统的驱动程序不兼容。
-   固件与操作系统组件不兼容。

如果硬件供应商决定实现其他逻辑来确定 Windows 是否已成功启动，这是可接受。 正如前面提到，预期结果是由固件作者的固件更新测试覆盖范围将阻止大部分危机导致的不兼容的固件。

## <a name="related-topics"></a>相关主题
[ESRT 表定义](esrt-table-definition.md)  
[Plug and play 设备](plug-and-play-device.md)  
[创作更新驱动程序包](authoring-an-update-driver-package.md)  
[处理更新](processing-updates.md)  
[设备 I/O 从 UEFI 环境](device-i-o-from-the-uefi-environment.md)  
[固件更新状态](firmware-update-status.md)  
