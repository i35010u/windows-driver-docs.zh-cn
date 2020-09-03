---
title: BCDEdit 选项参考
description: BCDEdit 选项参考
ms.assetid: 351f8bc3-a228-48a4-bda8-69ee8521a5d3
ms.date: 04/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: d0540791c5f2b2f5aa11c4072dc2165272d8a6fd
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384417"
---
# <a name="bcdedit-options-reference"></a>BCDEdit 选项参考

*启动项参数*或 *启动参数*是可选的，表示配置选项的特定于系统的设置。 可以将启动参数添加到操作系统的启动项。

本部分介绍与在基于 x86 和基于 x64 的处理器的计算机上开发、测试和调试驱动程序相关的 Windows 支持的 Windows 版本的启动选项。 可以将这些参数添加到 Windows 操作系统的启动条目。

> [!CAUTION]
> 需要管理权限才能使用 BCDEdit 来修改 BCD。 使用 BCDEdit /set 命令更改某些启动项目选项可能导致计算机无法运行。 请改为使用系统配置实用程序 (MSConfig.exe) 更改启动设置。
 
> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

 
## <a name="in-this-section"></a>在本节中

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="bcdedit--bootdebug.md" data-raw-source="[&lt;strong&gt;BCDEdit /bootdebug&lt;/strong&gt;](bcdedit--bootdebug.md)"><strong>BCDEdit /bootdebug</strong></a></p></td>
<td align="left"><p><strong>/Bootdebug</strong> boot 选项启用或禁用当前或指定的 Windows 操作系统启动项的启动调试。</p>
<blockquote>
[!Note]<br />
设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。
</blockquote>
 </td>
</tr>
<tr class="even">
<td align="left"><p><a href="bcdedit--dbgsettings.md" data-raw-source="[&lt;strong&gt;BCDEdit /dbgsettings&lt;/strong&gt;](bcdedit--dbgsettings.md)"><strong>BCDEdit /dbgsettings</strong></a></p></td>
<td align="left"><p><strong>/Dbgsettings</strong>选项设置或显示计算机的当前全局调试器设置。 若要启用或禁用内核调试器，请使用 <a href="bcdedit--debug.md" data-raw-source="[&lt;strong&gt;BCDEdit /debug&lt;/strong&gt;](bcdedit--debug.md)"><strong>BCDEdit/debug</strong></a> 选项。</p>
<blockquote>
[!Note]<br />
设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。
</blockquote>
 </td>
</tr>
<tr class="odd">
<td align="left"><p><a href="bcdedit--debug.md" data-raw-source="[&lt;strong&gt;BCDEdit /debug&lt;/strong&gt;](bcdedit--debug.md)"><strong>BCDEdit /debug</strong></a></p></td>
<td align="left"><p><strong>/Debug</strong> boot 选项启用或禁用与指定启动项或当前启动项关联的 Windows 操作系统的内核调试。</p>
<blockquote>
[!Note]<br />
设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。
</blockquote>
 </td>
</tr>
<tr class="even">
<td align="left"><p><a href="bcdedit--deletevalue.md" data-raw-source="[&lt;strong&gt;BCDEdit /deletevalue&lt;/strong&gt;](bcdedit--deletevalue.md)"><strong>BCDEdit /deletevalue</strong></a></p></td>
<td align="left"><p><strong>BCDEdit/deletevalue</strong>命令从 Windows 启动配置数据存储 (BCD) 中删除或删除启动项选项 (及其值) 。 使用 <strong>bcdedit/deletevalue</strong> 命令删除使用 <a href="bcdedit--set.md" data-raw-source="[&lt;strong&gt;BCDEdit /set&lt;/strong&gt;](bcdedit--set.md)"><strong>bcdedit/set</strong></a> 命令添加的选项。 为 Windows 7、Windows 8、Windows 8.1、Windows 10 和更高版本的 windows 测试和调试驱动程序时，可能需要删除启动项选项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="bcdedit--ems.md" data-raw-source="[&lt;strong&gt;BCDEdit /ems&lt;/strong&gt;](bcdedit--ems.md)"><strong>BCDEdit /ems</strong></a></p></td>
<td align="left"><p><strong>/Ems</strong>选项启用或禁用指定操作系统启动条目 (ems) 的紧急管理服务。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="bcdedit--emssettings.md" data-raw-source="[&lt;strong&gt;BCDEdit /emssettings&lt;/strong&gt;](bcdedit--emssettings.md)"><strong>BCDEdit /emssettings</strong></a></p></td>
<td align="left"><p><strong>/Emssettings</strong>选项为计算机设置全局紧急管理服务 (EMS) 设置。 若要启用或禁用 EMS，请使用 <strong>/ems</strong> 选项。 对于任何启动项， <strong>/emssettings</strong> 选项不会启用或禁用 EMS。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="bcdedit--set.md" data-raw-source="[&lt;strong&gt;BCDEdit /set&lt;/strong&gt;](bcdedit--set.md)"><strong>BCDEdit /set</strong></a></p></td>
<td align="left"><p><strong>BCDEdit/set</strong>命令在 windows 7、windows server 2008、windows 8、Windows 8.1、windows 10、windows server 2012 和 windows Server 2012 R2 (BCD) 的 windows 启动配置数据存储中设置启动条目选项值。 使用 BCDEdit /set 命令可配置特定的启动项目元素，如内核调试程序设置、内存选项或启用测试签名的内核模式代码或负载备用硬件抽象层 (HAL) 的选项和内核文件。 若要删除启动项目选项，请使用 <a href="bcdedit--deletevalue.md" data-raw-source="[&lt;strong&gt;BCDEdit /deletevalue&lt;/strong&gt;](bcdedit--deletevalue.md)">BCDEdit/deletevalue</a> 命令。</p></td>
</tr>
</tbody>
</table>

 ## <a name="see-also"></a>另请参阅
 
 [添加启动项](./adding-boot-entries.md)