---
title: 无缝危机预防和恢复
description: 如果固件更新失败，则结果可能是灾难性的。
ms.date: 08/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8e625e3bac61e953ade013d826e1a2bf76981029
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783593"
---
# <a name="seamless-crisis-prevention-and-recovery"></a>无缝危机预防和恢复


如果固件更新失败，则结果可能是灾难性的。 最重要的是，更新将会失败，但系统会复原并恢复，最终用户不会意识到这一点。 在最糟糕的情况下，失败的固件更新可能导致完全不可用的系统，要求最终用户将其系统返回给零售商或制造商进行修复。 后一种情况就是我们称之为 *危机* 的情况。

由于固件更新失败或者固件与 Windows 或系统的其他方面不兼容，可能会导致危机。 本部分介绍了一些功能，这些功能旨在防止固件更新失败并从危机恢复。 我们的期望是固件作者的固件更新测试覆盖率会阻止不兼容固件导致的大多数危机。

为了向最终用户提供良好的体验，固件驱动程序包更新机制必须满足以下危机防护和恢复要求。 这些要求不会妨碍其他危机防护或恢复解决方案。

## <a name="pre-installation-criteria"></a>安装前条件


当系统固件执行实际更新时，必须执行一系列的预安装检查。 系统固件必须执行此检查以确保有足够的功率来完成更新。 还建议在应用更新之前对每个更新进行检查（如果有多个固件更新）。 下面提供了要检查和验证的项的列表。 所有检查都必须在适用的情况下执行。 执行测试没有特定的顺序。

<table>
<colgroup>
<col width="20%" />
<col width="80%" />
</colgroup>
<thead>
<tr class="header">
<th>检查类型</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>强力</td>
<td><ul>
<li>系统必须有至少25% 的电池电量。</li>
<li>受限 power (通过 USB 电缆和/或 AC power) 供电，不是必需的。</li>
</ul>
<div class="alert">
<strong>注意</strong>  在测试/实验室环境中，只要提供受限电源，就可以不存在电池，但仍允许更新固件。 但是，必须在死电池和不收费电池之间进行区分，并且不存在电池。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td>安全性</td>
<td><ul>
<li>验证 update 胶囊负载已正确签名。</li>
<li>验证有效负载中任何基于 PE 的 EFI 文件是否使用适当的 EFI 证书进行了正确签名。</li>
</ul></td>
</tr>
<tr class="odd">
<td>完整性</td>
<td><p>在固件更新负载上执行完整性检查。</p></td>
</tr>
<tr class="even">
<td>版本</td>
<td><p>验证要应用的固件是否不会将当前的已安装固件降级到 LowestSupportedFirmwareVersion 值之外。</p></td>
</tr>
<tr class="odd">
<td>存储</td>
<td><p>根据系统的硬件，将根据需要执行以下检查</p>
<ul>
<li>当前固件的备份有足够的空间，将被替换</li>
<li>设备上有足够的空间可容纳新固件</li>
</ul></td>
</tr>
</tbody>
</table>

 

任何故障都必须产生适当的上一次尝试状态错误代码。 有关详细信息，请参阅 [ESRT 表定义](esrt-table-definition.md) 和 [固件更新状态](firmware-update-status.md)中的上次尝试状态错误代码信息。

如果正在应用多个更新并且某些操作通过了预安装检查，而另一些则未通过，则平台固件可以继续更新通过预安装检查的资源的固件。 但是，不能更新未通过预安装检查的任何资源。

## <a name="post-installation-criteria"></a>安装后条件

安装固件 (设备或系统) 之后，必须对其进行检查，以验证新更新的固件映像是否适用。 这是为了最大程度地减少在实际更新过程中引入的任何损坏的风险 (例如，flash ROM 中的粘滞位、更新期间总线上的噪音，等等) 。

更新过程必须验证更新的固件是否通过完整性检查。 如果该操作失败，则必须通过回滚到最近一次已知的固件版本来恢复。

任何故障都必须产生适当的上一次尝试状态错误代码。 有关详细信息，请参阅 [ESRT 表定义](esrt-table-definition.md) 和 [固件更新状态](firmware-update-status.md)中的上次尝试状态错误代码信息。

## <a name="recovering-from-install-and-boot-failures"></a>从安装和启动故障中恢复

若要防止系统进入无法启动状态，固件更新机制必须满足以下要求，以防固件更新安装失败，或者系统无法成功启动的情况。

> [!NOTE]
> 在以下部分中，术语 "已提交" 用于描述固件。 固件提交后，固件被视为完全安装，并且由于启动故障等原因，固件不会自动回滚固件。 "未提交" 的固件介绍部分更新的固件，并且可能会在固件更新无法完成或更新固件检测到故障的情况下回滚到以前的版本 (例如，更新) 中的 CRC 检查无效。 固件是否提交是固件应在内部跟踪的内容，并且不是作为 ESRT 的一部分捕获的。

### <a name="firmware-update-unsuccessful"></a>固件更新失败

如果无法安装单个系统或设备固件，或者安装不正确 (例如，由于某种类型的损坏，或者在安装更新) 时断电，则更新可能会重试最多三个 (3) 次，包括第一次尝试。 如果固件将执行其他重试尝试，则在任何尝试之间，系统不得启动到 Windows 中。 如果所有尝试都失败，则更新固件必须放弃更新。 如果更新已部分应用，则固件必须回滚到以前的版本。 固件必须回滚到以前的版本，而无需任何用户交互。 更新失败不会影响其他挂起的更新;应尝试挂起的固件更新。

在处理完所有更新后，UEFI 将继续启动 Windows。 UEFI 固件必须验证是否已成功安装任何未提交的固件更新，以减轻电源丢失的问题， (UEFI 应始终不会尝试通过部分写入的固件) 启动 Windows。

安装失败的可能原因包括但不限于：

-   资源不足
-   断电
-   硬件故障

### <a name="firmware-update-succeeds-but-windows-fails-to-boot"></a>固件更新成功，但 Windows 无法启动

在提交更新的固件后，UEFI 固件不负责回滚该固件。 Windows 中的现有故障转移逻辑会将最终用户转移到 Windows 恢复环境，在两次不成功的启动尝试之后 (WinRE) 。 WinRE 可能会也可能不会成功启动。 最终用户必须采取手动恢复步骤来恢复其系统，或者必须将其设备返还给零售商/制造商。

此类故障的可能原因包括但不限于：

-   固件与操作系统驱动程序不兼容。
-   固件与 OS 组件不兼容。

如果硬件供应商决定实现其他逻辑来确定 Windows 是否已成功启动，则可接受。 如前文所述，预期是固件作者的固件更新测试覆盖率会阻止不兼容固件导致的大多数危机。

## <a name="related-topics"></a>相关主题
[ESRT 表定义](esrt-table-definition.md)  
[即插即用设备](plug-and-play-device.md)  
[创作更新驱动程序包](authoring-an-update-driver-package.md)  
[处理更新](processing-updates.md)  
[来自 UEFI 环境的设备 I/O](device-i-o-from-the-uefi-environment.md)  
[固件更新状态](firmware-update-status.md)  
