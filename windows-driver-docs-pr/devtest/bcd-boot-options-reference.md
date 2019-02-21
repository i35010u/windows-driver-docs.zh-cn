---
title: BCDEdit 选项参考
description: BCDEdit 选项参考
ms.assetid: 351f8bc3-a228-48a4-bda8-69ee8521a5d3
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1da864941f44a44e98834848d2dc4e1fde37754d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519830"
---
# <a name="bcdedit-options-reference"></a>BCDEdit 选项参考


*启动入口参数*，或*引导参数*，是可选的系统特定的设置，表示配置选项。 可以向操作系统的启动项来添加启动参数。

本部分介绍支持的与开发、 测试和调试基于 x86 和基于 x64 的处理器的计算机上的驱动程序相关的 Windows 版本的启动选项。 可以将这些参数添加到 Windows 操作系统的启动项。

> [!NOTE]
> 设置 BCDEdit 选项之前，您可能需要禁用或暂停 BitLocker 和安全启动的计算机上。

 

## <a name="in-this-section"></a>本部分内容


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
<td align="left"><p><a href="bcdedit--bootdebug.md" data-raw-source="[&lt;strong&gt;BCDEdit /bootdebug&lt;/strong&gt;](bcdedit--bootdebug.md)"><strong>BCDEdit /bootdebug</strong></a></p></td>
<td align="left"><p><strong>/Bootdebug</strong>启动选项启用或禁用的当前或指定 Windows 操作系统启动项目的调试启动。</p>
<blockquote>
[!Note]<br />
设置 BCDEdit 选项之前，您可能需要禁用或暂停 BitLocker 和安全启动的计算机上。
</blockquote>
 </td>
</tr>
<tr class="even">
<td align="left"><p><a href="bcdedit--dbgsettings.md" data-raw-source="[&lt;strong&gt;BCDEdit /dbgsettings&lt;/strong&gt;](bcdedit--dbgsettings.md)"><strong>BCDEdit /dbgsettings</strong></a></p></td>
<td align="left"><p><strong>/Dbgsettings</strong>选项设置，或显示计算机的当前全局调试器设置。 若要启用或禁用内核调试程序，请使用<a href="bcdedit--debug.md" data-raw-source="[&lt;strong&gt;BCDEdit /debug&lt;/strong&gt;](bcdedit--debug.md)"> <strong>BCDEdit /debug</strong> </a>选项。</p>
<blockquote>
[!Note]<br />
设置 BCDEdit 选项之前，您可能需要禁用或暂停 BitLocker 和安全启动的计算机上。
</blockquote>
 </td>
</tr>
<tr class="odd">
<td align="left"><p><a href="bcdedit--debug.md" data-raw-source="[&lt;strong&gt;BCDEdit /debug&lt;/strong&gt;](bcdedit--debug.md)"><strong>BCDEdit /debug</strong></a></p></td>
<td align="left"><p><strong>/Debug</strong>启动选项启用或禁用内核调试与指定的启动项目或当前引导条目相关联的 Windows 操作系统。</p>
<blockquote>
[!Note]<br />
设置 BCDEdit 选项之前，您可能需要禁用或暂停 BitLocker 和安全启动的计算机上。
</blockquote>
 </td>
</tr>
<tr class="even">
<td align="left"><p><a href="bcdedit--deletevalue.md" data-raw-source="[&lt;strong&gt;BCDEdit /deletevalue&lt;/strong&gt;](bcdedit--deletevalue.md)"><strong>BCDEdit /deletevalue</strong></a></p></td>
<td align="left"><p><strong>BCDEdit /deletevalue</strong>命令删除，或从 Windows 引导配置数据存储 (BCD) 中删除的启动项选项 （和其值）。 使用<strong>BCDEdit /deletevalue</strong>命令删除已添加使用的选项<a href="bcdedit--set.md" data-raw-source="[&lt;strong&gt;BCDEdit /set&lt;/strong&gt;](bcdedit--set.md)"> <strong>BCDEdit /set</strong> </a>命令。 可能需要在测试和调试您的驱动程序的 Windows 7、 Windows 8、 Windows 8.1，Windows 10 和更高版本的 Windows 时删除启动条目选项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="bcdedit--ems.md" data-raw-source="[&lt;strong&gt;BCDEdit /ems&lt;/strong&gt;](bcdedit--ems.md)"><strong>BCDEdit /ems</strong></a></p></td>
<td align="left"><p><strong>/Ems</strong>选项启用或禁用紧急管理服务 (EMS) 为指定的操作系统启动项目。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="bcdedit--emssettings.md" data-raw-source="[&lt;strong&gt;BCDEdit /emssettings&lt;/strong&gt;](bcdedit--emssettings.md)"><strong>BCDEdit /emssettings</strong></a></p></td>
<td align="left"><p><strong>/Emssettings</strong>选项设置为计算机的全局紧急管理服务 (EMS) 设置。 若要启用或禁用 EMS，请使用<strong>/ems</strong>选项。 <strong>/Emssettings</strong>选项不会启用或禁用的任何启动项的 EMS。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="bcdedit--set.md" data-raw-source="[&lt;strong&gt;BCDEdit /set&lt;/strong&gt;](bcdedit--set.md)"><strong>BCDEdit /set</strong></a></p></td>
<td align="left"><p><strong>BCDEdit /set</strong>命令设置 Windows 引导配置数据存储 (BCD) Windows 7、 Windows Server 2008、 Windows 8、 Windows 8.1，Windows 10、 Windows Server 2012 和 Windows Server 2012 R2 中的启动项选项值。 使用<strong>BCDEdit /set</strong>命令来配置特定的启动项元素，如内核调试程序设置、 内存选项或启用测试签名的内核模式代码或负载备用硬件抽象层 (HAL) 的选项和内核文件。 若要删除的启动项选项，请使用<a href="bcdedit--deletevalue.md" data-raw-source="[&lt;strong&gt;BCDEdit /deletevalue&lt;/strong&gt;](bcdedit--deletevalue.md)"> <strong>BCDEdit /deletevalue</strong> </a>命令。</p></td>
</tr>
</tbody>
</table>

 

### <a name="mapping-bootini-options-to-bcdedit-options-and-elements"></a>Boot.ini 选项映射到 BCDEdit 选项和元素

下表提供从使用中 （在 Boot.ini)，Windows Vista 之前的操作系统的启动选项到 BCDEdit 选项和在 Windows 中使用的 BCD 元素之间映射。 璝惠 BCD 启动元素，请参见[BCD 引用](https://go.microsoft.com/fwlink/p/?linkid=56420)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Boot.ini</th>
<th align="left">BCDEdit 选项</th>
<th align="left">BCD 元素类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>/3GB</p></td>
<td align="left"><p><strong>increaseuserva</strong></p></td>
<td align="left"><p>BcdOSLoaderInteger_IncreaseUserVa</p></td>
</tr>
<tr class="even">
<td align="left"><p>/BASEVIDEO</p></td>
<td align="left"><p><strong>vga</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_UseVgaDriver</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/ BOOTLOG</p></td>
<td align="left"><p><strong>bootlog</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_BootLogInitialization</p></td>
</tr>
<tr class="even">
<td align="left"><p>/BREAK</p></td>
<td align="left"><p><strong>halbreakpoint</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_DebuggerHalBreakpoint</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/CRASHDEBUG</p></td>
<td align="left"><p><strong>/dbgsettings /start</strong></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>/ 调试 BOOTDEBUG</p></td>
<td align="left"><p><strong>/debug</strong></p>
<p><strong>/bootdebug</strong></p></td>
<td align="left"><p>BcdLibraryBoolean_DebuggerEnabled</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/DEBUG</p></td>
<td align="left"><p><strong>/debug</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_KernelDebuggerEnabled</p></td>
</tr>
<tr class="even">
<td align="left"><p>/ 调试，/DEBUGPORT =</p></td>
<td align="left"><p><strong>/dbgsettings</strong></p></td>
<td align="left"><p>BcdLibraryInteger_DebuggerType</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/DEBUGPORT=</p></td>
<td align="left"><p><strong>/dbgsettings</strong></p></td>
<td align="left"><p>BcdLibraryInteger_SerialDebuggerPort</p>
<p>BcdLibraryInteger_SerialDebuggerBaudRate</p>
<p>BcdLibraryInteger_1394DebuggerChannel</p>
<p>BcdLibraryString_UsbDebuggerTargetName</p>
<p>BcdLibraryInteger_DebuggerNetHostIP</p>
<p>BcdLibraryInteger_DebuggerNetPort</p>
<p>BcdLibraryBoolean_DebuggerNetDhcp</p>
<p>BcdLibraryString_DebuggerNetKey</p></td>
</tr>
<tr class="even">
<td align="left"><p>/EXECUTE</p></td>
<td align="left"><p><strong>nx</strong></p></td>
<td align="left"><p>BcdOSLoaderInteger_NxPolicy</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/FASTDETECT</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>/HAL=</p></td>
<td align="left"><p><strong>hal</strong></p></td>
<td align="left"><p>BcdOSLoaderString_HalPath</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/KERNEL=</p></td>
<td align="left"><p><strong>kernel</strong></p></td>
<td align="left"><p>BcdOSLoaderString_KernelPath</p></td>
</tr>
<tr class="even">
<td align="left"><p>/MAXMEM=</p></td>
<td align="left"><p><strong>truncatememory</strong></p></td>
<td align="left"><p>BcdLibraryInteger_TruncatePhysicalMemory</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/NODEBUG</p></td>
<td align="left"><p><strong>/debug</strong></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>/NOEXECUTE</p></td>
<td align="left"><p><strong>nx</strong> {</p></td>
<td align="left"><p>BcdOSLoaderInteger_NxPolicy</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/NOGUIBOOT</p></td>
<td align="left"><p><strong>quietboot</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_DisableBootDisplay</p></td>
</tr>
<tr class="even">
<td align="left"><p>/NOLOWMEM</p></td>
<td align="left"><p><strong>nolowmem</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_NoLowMemory</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/NOPAE</p></td>
<td align="left"><p><strong>pae</strong></p></td>
<td align="left"><p>BcdOSLoaderInteger_PAEPolicy</p></td>
</tr>
<tr class="even">
<td align="left"><p>/ONECPU</p></td>
<td align="left"><p><strong>onecpu</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_UseBootProcessorOnly</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/PAE</p></td>
<td align="left"><p><strong>pae</strong></p></td>
<td align="left"><p>BcdOSLoaderInteger_PAEPolicy</p></td>
</tr>
<tr class="even">
<td align="left"><p>/ PCILOCK</p></td>
<td align="left"><p><strong>usefirmwarepcisettings</strong></p></td>
<td align="left"><p>BcdOSLoaderInteger_UseFirmwarePciSettings</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/ 重定向</p></td>
<td align="left"><p><strong>/ems</strong></p>
<p><strong>/emssettings</strong> [ <strong>BIOS</strong> ] |</p>
<p>[ <strong>EMSPORT:</strong>{<em>端口</em>} |[<strong>EMSBAUDRATE:</strong> {<em>baudrate</em>}]]</p></td>
<td align="left"><p>BcdOSLoaderBoolean_EmsEnabled</p></td>
</tr>
<tr class="even">
<td align="left"><p>/SOS</p></td>
<td align="left"><p><strong>sos</strong></p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 ## <a name="see-also"></a>另请参阅
 
 [添加启动项](https://docs.microsoft.com/windows-hardware/drivers/devtest/adding-boot-entries)

 

 





