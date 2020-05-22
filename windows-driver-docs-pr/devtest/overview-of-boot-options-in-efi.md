---
title: EFI 中的启动选项概述
description: EFI 中的启动选项概述
ms.assetid: 2237d321-75e6-4723-9f08-484bd9097360
keywords:
- NVRAM 启动选项 WDK，关于 EFI NVRAM boot 选项
- EFI NVRAM 启动选项 WDK，关于 EFI NVRAM boot 选项
- 全局定义的变量 WDK 启动选项
- 启动选项 WDK，变量
- 启动项 Id WDK
- EFI 启动项 Id WDK
- 标识符 WDK 启动选项
- 启动条目 WDK
- Bootcfg 工具
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5542f5a30344ff56fdad1ef4c68d48a77b80b7f0
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769563"
---
# <a name="overview-of-boot-options-in-efi"></a>EFI 中的启动选项概述

与 BIOS 固件系统上的启动选项类似，EFI NVRAM 中有两种类型的启动选项：

-   *全局定义的变量*，适用于计算机上所有可启动的设备和可启动的程序。

-   仅适用于可启动设备或程序的特定负载配置的*启动选项变量*，如操作系统。 系统特定的变量包括计算机上可启动设备或可启动程序的每个配置的启动项。

在[efi 中编辑启动选项](editing-boot-options-in-efi.md)中讨论的[Bootcfg](https://docs.microsoft.com/windows-server/administration/windows-commands/bootcfg)工具允许你查看和编辑 efi NVRAM 中的启动选项。

下面的示例演示具有 Itanium 处理器的计算机的 Bootcfg 显示。

```
Boot Options
------------
Timeout:             30
Default:             \Device\HarddiskVolume3\WINDOWS
CurrentBootEntryID:  1

Boot Entries
------------

Boot entry ID:    1
OS Friendly Name: Windows Server 2003, Enterprise
OsLoadOptions: /debug /debugport=COM1 /baudrate=57600
BootFilePath:     \Device\HarddiskVolume1\EFI\Microsoft\WINNT50\ia64ldr.efi
OsFilePath:       \Device\HarddiskVolume3\WINDOWS

Boot entry ID:    2
OS Friendly Name: EFI Shell [Built-in]
```

下表描述了在 EFI NVRAM 中启动数据的 Bootcfg 显示元素。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">说明</th>
<th align="left">示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>启动选项</strong></p></td>
<td align="left"><p>包含适用于所有启动项的选项。</p></td>
<td align="left"><p>（节标题）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>超时</strong></p></td>
<td align="left"><p>确定启动菜单的显示时间。 如果该值过期，启动加载程序将加载默认操作系统。</p></td>
<td align="left"><pre space="preserve"><code>Timeout:   30</code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>默认</strong></p></td>
<td align="left"><p>指定默认操作系统的位置。</p></td>
<td align="left"><pre space="preserve"><code>\Device\HarddiskVolume3\WINDOWS</code></pre></td>
</tr>
<tr class="even">
<td align="left"><p><strong>CurrentBootEntryID</strong></p></td>
<td align="left"><p>标识用于启动当前操作系统会话的启动项。</p></td>
<td align="left"><pre space="preserve"><code>CurrentBootEntryID:  1</code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>启动项</strong></p></td>
<td align="left"><p>包含特定于系统的数据。 它包含计算机上安装的每个操作系统或可启动程序的一个或多个<em>启动项</em>。</p>
<p><em>启动项</em>是一组用于定义操作系统或可启动程序的加载配置的选项。</p></td>
<td align="left"><p>（节标题）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>启动项 ID</strong></p></td>
<td align="left"><p>向 Bootcfg 标识启动项。 重新排序启动条目时，此值会发生更改。</p>
<p>这不是<em>efi 启动项 ID</em>，它是 efi 组件的永久性标识符。</p></td>
<td align="left"><pre space="preserve"><code>Boot entry ID:    1</code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>OS 友好名称</strong></p></td>
<td align="left"><p>表示启动菜单中的启动项。</p></td>
<td align="left"><pre space="preserve"><code>Windows Server 2003,
Enterprise</code></pre></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OsLoadOptions</strong></p></td>
<td align="left"><p>指定项的<em>启动参数</em>。 <em>启动参数</em>是用于启用、禁用和配置操作系统功能的命令。 EFI 启动管理器将这些参数传递给可启动设备或系统，以进行解释和实施。</p>
<p>有关与驱动程序调试和测试相关的启动参数的列表，请参阅 boot.ini<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-options-in-a-boot-ini-file" data-raw-source="[Boot Options in a Boot.ini File](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-options-in-a-boot-ini-file)">文件中的启动选项</a>。</p></td>
<td align="left"><pre space="preserve"><code>OsLoadOptions: /debug
/debugport=COM1 /baudrate=57600</code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>BootFilePath</strong></p></td>
<td align="left"><p>指定操作系统的 EFI 启动加载器的位置。 在基于 EFI 的系统上，每个操作系统或可启动设备在 EFI 分区上都有自己的启动加载器副本。</p>
<p>在 EFI NVRAM 中，启动加载器文件路径存储为二进制 EFI 设备路径，该路径使用全局唯一标识符（GUID）来标识 EFI 分区。</p>
<p>Bootcfg 在路径显示中使用分区的 NT 设备名称。</p></td>
<td align="left"><pre space="preserve"><code>BootFilePath: \Device\HarddiskVolume1
\EFI\Microsoft\WINNT50\ia64ldr.efi</code></pre></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OsFilePath</strong></p></td>
<td align="left"><p>指定操作系统的位置。</p>
<p>在 NVRAM 中，此值存储为 EFI 设备路径，该路径使用启动磁盘分区的 GUID 和包含操作系统的目录的路径。</p>
<p>Bootcfg 在路径显示中使用分区的 NT 设备名称。</p></td>
<td align="left"><pre space="preserve"><code>OsFilePath: \Device\HarddiskVolume3
\WINDOWS</code></pre></td>
</tr>
</tbody>
</table>

此外，还存在一个用于 Bootcfg 不显示的 EFI 启动项的重要元素，即*efi 启动项 ID*。 EFI 启动条目是 EFI 启动条目的唯一标识符。 此标识符是在创建启动项时分配的，并且不会更改。 它表示多个列表中的启动项（包括*BootOrder*数组），它是磁盘上的目录的名称，系统在该目录中存储与启动项相关的数据，包括启动项的备份副本。 EFI 启动项 ID 的格式为 Boot*xxxx*，其中*xxxx*是一个十六进制数，用于反映创建启动条目的顺序。

> [!NOTE] 
> Bootcfg 中的**启动项 ID**字段和 Nvrboot 中的启动条目号不显示 EFI 启动项 id。 Bootcfg 和 Nvrboot Id 是表示启动**条目**部分中启动项顺序的行号，并在重新排序项时进行更改。

有关基于 Itanium 的系统上的启动选项的详细说明，请参阅可扩展固件接口规范。 可以从[Intel 可扩展固件接口](https://www.intel.com/content/www/us/en/architecture-and-technology/unified-extensible-firmware-interface/efi-homepage-general-technology.html)网站下载规范的副本。
