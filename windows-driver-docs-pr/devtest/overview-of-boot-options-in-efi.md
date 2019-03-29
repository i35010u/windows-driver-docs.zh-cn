---
title: EFI 中的启动选项概述
description: EFI 中的启动选项概述
ms.assetid: 2237d321-75e6-4723-9f08-484bd9097360
keywords:
- NVRAM 启动选项 WDK，有关 EFI NVRAM 启动选项
- EFI NVRAM 启动选项 WDK，有关 EFI NVRAM 启动选项
- 全局定义的变量 WDK 启动选项
- 启动选项 WDK，变量
- 启动项目 Id WDK
- EFI 启动项 Id WDK
- 标识符 WDK 启动选项
- 启动项 WDK
- Bootcfg 工具
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: d43b51305430f823e7bba91990343e9e5f02c474
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562357"
---
# <a name="overview-of-boot-options-in-efi"></a>EFI 中的启动选项概述

类似于使用 BIOS 固件的系统上启动选项，有两种类型的 EFI NVRAM 中的启动选项：

-   *全局定义的变量*适用于所有可启动的设备和计算机上的可启动程序。

-   *启动选项变量*仅适用于特定的负载配置的可启动的设备或程序，例如操作系统。 特定于系统变量包含可启动的设备或计算机上的可启动程序的每个配置的启动项。

[Bootcfg](https://docs.microsoft.com/windows-server/administration/windows-commands/bootcfg)工具中所述[在 EFI 中编辑启动选项](editing-boot-options-in-efi.md)允许您查看和编辑 EFI NVRAM 中的启动选项。

下面的示例显示的 Bootcfg 配有 Itanium 处理器的计算机。

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

下表描述的 EFI NVRAM 中启动数据 Bootcfg 显示的元素。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">描述</th>
<th align="left">示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>启动选项</strong></p></td>
<td align="left"><p>包含适用于所有启动项的选项。</p></td>
<td align="left"><p>（部分标头）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Timeout</strong></p></td>
<td align="left"><p>确定启动菜单显示的时间。 此值过期后，启动加载程序将加载默认操作系统。</p></td>
<td align="left"><pre space="preserve"><code>Timeout:   30</code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>默认</strong></p></td>
<td align="left"><p>指定的默认操作系统的位置。</p></td>
<td align="left"><pre space="preserve"><code>\Device\HarddiskVolume3\WINDOWS</code></pre></td>
</tr>
<tr class="even">
<td align="left"><p><strong>CurrentBootEntryID</strong></p></td>
<td align="left"><p>标识用于启动操作系统的当前会话的启动项目。</p></td>
<td align="left"><pre space="preserve"><code>CurrentBootEntryID:  1</code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>启动项</strong></p></td>
<td align="left"><p>包含特定于系统的数据。 它包含一个或多个<em>引导条目</em>为每个操作系统或可启动的计算机上安装的程序。</p>
<p>一个<em>引导条目</em>是一组定义的操作系统或可启动的程序的负载配置的选项。</p></td>
<td align="left"><p>（部分标头）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>启动项目 ID</strong></p></td>
<td align="left"><p>标识到 Bootcfg 的启动项目。 此值更改时重新排序的启动项。</p>
<p>这不是<em>EFI 启动项 ID</em>，这是 EFI 组件的永久标识符。</p></td>
<td align="left"><pre space="preserve"><code>Boot entry ID:    1</code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>操作系统的好记名称</strong></p></td>
<td align="left"><p>表示在启动菜单中的启动项目。</p></td>
<td align="left"><pre space="preserve"><code>Windows Server 2003,
Enterprise</code></pre></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OsLoadOptions</strong></p></td>
<td align="left"><p>指定<em>引导参数</em>的项。 <em>引导参数</em>是命令，用于启用、 禁用和配置操作系统功能。 EFI 启动管理器将这些参数传递给可启动的设备或系统，以解释并实现。</p>
<p>有关与驱动程序调试和测试相关的启动参数的列表，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-options-in-a-boot-ini-file" data-raw-source="[Boot Options in a Boot.ini File](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-options-in-a-boot-ini-file)">Boot.ini 文件中的启动选项</a>。</p></td>
<td align="left"><pre space="preserve"><code>OsLoadOptions: /debug
/debugport=COM1 /baudrate=57600</code></pre></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>BootFilePath</strong></p></td>
<td align="left"><p>指定操作系统 EFI 启动加载器的位置。 在基于 EFI 的系统中，情况下，每个操作系统或可启动的设备有其自己的启动加载器副本在 EFI 分区上。</p>
<p>EFI NVRAM 中的启动加载程序文件路径存储为二进制 EFI 设备路径使用全局唯一标识符 (GUID) 识别 EFI 分区。</p>
<p>Bootcfg 使用 NT 设备名称的分区在其路径显示。</p></td>
<td align="left"><pre space="preserve"><code>BootFilePath: \Device\HarddiskVolume1
\EFI\Microsoft\WINNT50\ia64ldr.efi</code></pre></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OsFilePath</strong></p></td>
<td align="left"><p>指定操作系统的位置。</p>
<p>在 NVRAM，此值存储为使用启动磁盘分区的 GUID 的 EFI 设备路径和包含操作系统的目录的路径。</p>
<p>Bootcfg 使用 NT 设备名称的分区在其路径显示。</p></td>
<td align="left"><pre space="preserve"><code>OsFilePath: \Device\HarddiskVolume3
\WINDOWS</code></pre></td>
</tr>
</tbody>
</table>

此外，还有 Bootcfg 不会显示的 EFI 启动项的一个重要元素*EFI 启动项 ID*。 EFI 启动项是 EFI 启动项的唯一标识符。 此标识符时创建的启动项目，并且不会更改分配。 表示多个列表，包括中的启动项目*BootOrder*数组，也是如此系统将存储到的启动项目，包括启动项目的备份副本相关的数据磁盘上目录的名称。 EFI 启动项 ID 格式，启动*xxxx*，其中*xxxx*是一个十六进制数字，反映了在其中创建的启动项的顺序。

> [!NOTE] 
> **启动项目 ID** Bootcfg 中的字段和启动 Nvrboot 中的项数不显示 EFI 启动项目 id。 Bootcfg 和 Nvrboot Id 所表示的启动项目中的顺序的行号**启动项**部分，并更改时重新排序项。

有关在基于 Itanium 的系统上的启动选项的详细说明，请参阅可扩展固件接口规范。 可以下载一份从规范[Intel 可扩展固件接口](https://go.microsoft.com/fwlink/p/?linkid=10596)网站。
