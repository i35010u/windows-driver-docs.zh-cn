---
title: Boot.ini 文件中的启动选项
description: Boot.ini 是位于系统分区根目录的文本文件，通常是 c:\Boot.ini。 对于带有 BIOS 固件的计算机（在传统上，是具有 x86 和基于 x64 的处理器的计算机），boot.ini 将存储启动选项。
ms.assetid: a2593b6d-03df-49d1-ae77-efec4c2ac8be
keywords:
- Boot.ini 文件 WDK
- 启动选项 WDK，Boot.ini 文件
ms.date: 04/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 57e80e1002ee7a464682edac0bfc01f40f410354
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769685"
---
# <a name="boot-options-in-a-bootini-file"></a>Boot.ini 文件中的启动选项

> [!IMPORTANT] 
> 本主题介绍 Windows XP 和 Windows Server 2003 中支持的启动选项。 如果要更改 Windows 8、Windows Server 2012、Windows 7、Windows Server 2008 或 Windows Vista 的启动选项，请参阅[Windows vista 和更高版本中的启动选项](boot-options-in-windows-vista-and-later.md)。\]

Boot.ini 是位于系统分区根目录（通常为 c： Boot.ini）的文本文件 \\ 。 对于带有 BIOS 固件的计算机（在传统上，具有基于 IA-32 和基于 x64 的处理器）的计算机，boot.ini 存储启动选项。 在 Windows Server 2003 和更早版本的 Windows NT 操作系统上，当计算机启动时，Windows 启动加载程序（称为 "ntldr"）读取 Boot.ini 文件并在启动菜单中显示每个操作系统的条目。 然后，ntldr 按照 Boot.ini 文件中的设置加载所选操作系统。

默认情况下，NTFS 驱动器上的 "**系统**"、"**隐藏**"、"**存档**" 和 "**只读**" 属性设置为 "保护 boot.ini";但是，Administrators 组的成员可以更改这些属性。 文件属性不影响启动加载程序的操作。

以下部分简要介绍了 Boot.ini，并说明了特定于具有个人计算机高级技术（PC/AT）类型 BIOS 固件的计算机的启动选项的各个方面。

本节包括：

- [Boot.ini 文件概述](overview-of-the-boot-ini-file.md)
- [编辑 Boot.ini 文件](editing-the-boot-ini-file.md)
- [备份 Boot.ini 文件](backing-up-the-boot-ini-file.md)

本文档介绍了对驱动程序开发人员和测试人员特别感兴趣的 Boot.ini 的各个方面。 有关 Boot.ini 参数的完整列表，请参阅 Microsoft 支持部门网站上的[适用于 WINDOWS XP 和 Windows Server 2003 Boot.ini 文件的可用交换机选项](https://support.microsoft.com/help/833721/available-switch-options-for-the-windows-xp-and-the-windows-server-200)主题。


## <a name="mapping-bootini-options-to-bcdedit-options-and-elements"></a>将 Boot.ini 选项映射到 BCDEdit 选项和元素

下表提供了从 Windows Vista 之前的操作系统中使用的启动选项（在 Boot.ini 中）到 BCDEdit 选项和 Windows 中使用的 BCD 元素的映射。 有关包含 WMI 上下文的 BCD 启动元素的信息，请参阅[BCD Wmi 提供程序参考](https://docs.microsoft.com/previous-versions/windows/desktop/bcd/bcd-reference)。

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
<td align="left"><p><strong>svga</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_UseVgaDriver</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/BOOTLOG</p></td>
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
<td align="left"><p><strong>/dbgsettings/start</strong></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>/DEBUG、BOOTDEBUG</p></td>
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
<td align="left"><p>/DEBUG、/DEBUGPORT =</p></td>
<td align="left"><p><strong>/dbgsettings</strong></p></td>
<td align="left"><p>BcdLibraryInteger_DebuggerType</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/DEBUGPORT =</p></td>
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
<td align="left"><p>/HAL =</p></td>
<td align="left"><p><strong>hal</strong></p></td>
<td align="left"><p>BcdOSLoaderString_HalPath</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/KERNEL =</p></td>
<td align="left"><p><strong>壳</strong></p></td>
<td align="left"><p>BcdOSLoaderString_KernelPath</p></td>
</tr>
<tr class="even">
<td align="left"><p>/MAXMEM =</p></td>
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
<td align="left"><p><strong>保持</strong></p></td>
<td align="left"><p>BcdOSLoaderInteger_PAEPolicy</p></td>
</tr>
<tr class="even">
<td align="left"><p>/ONECPU</p></td>
<td align="left"><p><strong>onecpu</strong></p></td>
<td align="left"><p>BcdOSLoaderBoolean_UseBootProcessorOnly</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/PAE</p></td>
<td align="left"><p><strong>保持</strong></p></td>
<td align="left"><p>BcdOSLoaderInteger_PAEPolicy</p></td>
</tr>
<tr class="even">
<td align="left"><p>/PCILOCK</p></td>
<td align="left"><p><strong>usefirmwarepcisettings</strong></p></td>
<td align="left"><p>BcdOSLoaderInteger_UseFirmwarePciSettings</p></td>
</tr>
<tr class="odd">
<td align="left"><p>/REDIRECT</p></td>
<td align="left"><p><strong>/ems</strong></p>
<p><strong>/emssettings</strong> [ <strong>BIOS</strong> ] |</p>
<p>[ <strong>EMSPORT：</strong>{<em>port</em>} |[<strong>EMSBAUDRATE：</strong> {<em>波特率</em>}]]</p></td>
<td align="left"><p>BcdOSLoaderBoolean_EmsEnabled</p></td>
</tr>
<tr class="even">
<td align="left"><p>/SOS</p></td>
<td align="left"><p><strong>sos</strong></p></td>
<td align="left"></td>
</tr>
</tbody>
</table>


