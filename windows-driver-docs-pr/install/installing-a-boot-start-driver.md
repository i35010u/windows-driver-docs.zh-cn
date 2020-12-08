---
title: 安装引导启动驱动程序
description: 安装引导启动驱动程序
keywords:
- 设备设置 WDK 设备安装，启动驱动程序
- 设备安装 WDK，启动驱动程序
- 安装设备 WDK，启动驱动程序
- 启动驱动程序 WDK 设备安装
- 启动驱动程序分发磁盘 WDK 设备安装
- 分发磁盘 WDK
- 平台特定的分发磁盘 WDK
- 跨平台分发磁盘 WDK
- 供应商提供的启动驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d459e424fe7eda2c7cb2a4bc9818b83aa4c6fdab
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813723"
---
# <a name="installing-a-boot-start-driver"></a>安装引导启动驱动程序





*启动驱动程序* 是设备的驱动程序，必须安装该驱动程序才能启动 Microsoft Windows 操作系统。 大多数引导启动驱动程序都包含在 Windows 中，在 windows 安装的文本模式安装阶段，Windows 会自动安装这些引导启动驱动程序。 如果设备的引导启动驱动程序未包含在 Windows 中，则用户可以在安装文本模式期间为设备安装其他供应商提供的启动驱动程序。

若要安装启动 Windows 所需的设备，但其驱动程序未包含在操作系统中，用户必须执行以下操作：

1.  安装设备硬件并打开计算机。

2.  开始 Windows 安装 (运行 Windows 安装程序) 。 在安装的文本模式阶段 () ，Windows 将显示一条消息，指示你可以按特定的 **F**_n_ 键来安装引导启动驱动程序。

3.  当 Windows 显示此消息时，按指定的 **F**_n_ 键安装引导启动驱动程序，然后插入启动启动 [驱动程序分发磁盘](#boot-start-driver-distribution-disk)。

**注意**  此过程演示如何安装不包含在 Windows 中的 "内置" 驱动程序。 不要使用此过程来替换或更新 Windows 附带的驱动程序。 请等待 Windows 启动并使用设备管理器在设备上执行 "更新驱动程序" 操作。



如果 Windows 无法启动，则显示的某些错误消息可能指示缺少启动启动驱动程序。 下表描述了几个错误消息和可能的原因。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">错误消息</th>
<th align="left">可能的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>启动设备不可访问</p></td>
<td align="left"><p>启动磁盘是需要不包含在 Windows 中的驱动程序的第三方大容量存储设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p>安装程序无法确定计算机类型</p></td>
<td align="left"><p>需要新的 HAL 驱动程序。 在大多数计算机上不会出现此错误，但可能会在高端服务器上出现此错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>安装程序在计算机上找不到任何硬盘驱动器</p></td>
<td align="left"><p>未加载硬盘所需的启动设备驱动程序。</p></td>
</tr>
</tbody>
</table>



### <a name="boot-start-driver-distribution-disk"></a><a href="" id="boot-start-driver-distribution-disk"></a> Boot-Start 驱动程序分发磁盘

*启动驱动程序分发磁盘* 是一种介质，如软盘或 u 盘，其中包含 *txtsetup.oem* 文件和相关的驱动程序文件。 *Txtsetup.oem* 文件是一个文本文件，其中包含一系列硬件组件、将复制到系统的分发磁盘上的文件列表，以及要创建的注册表项和值的列表。  (WDK) 中的 Windows 驱动程序工具包提供了一个示例 *txtsetup.oem* 文件，该文件在 \\ wdk 的 src 目录下。 有关 *txtsetup.oem* 文件的内容的详细信息，请参阅 [txtsetup.oem 文件格式](/previous-versions/ff553509(v=vs.85))。

以下要求和建议适用于特定于平台的分发磁盘：

- Windows Server 2003 和更早版本 (平台特定的分发磁盘) 

  对于驱动程序支持的每个平台，Windows 都需要一个特定于平台的分发磁盘。 平台特定的分发磁盘包含一个 *txtsetup.oem* 文件和相关的驱动程序文件。 *Txtsetup.oem* 文件必须位于分发磁盘的根目录中。

- 跨平台和平台特定的分发磁盘 (Windows Server 2003 Service Pack 1 (SP1) 和更高版本) 

  Windows 支持跨平台分发磁盘，其中包含两个或更多个特定于平台的 *txtsetup.oem* 文件以及相关的驱动程序文件。

  若要区分跨平台分发磁盘上的平台，请使用下表中列出的平台目录。

  <table>
  <colgroup>
  <col width="33%" />
  <col width="33%" />
  <col width="33%" />
  </colgroup>
  <thead>
  <tr class="header">
  <th align="left">平台</th>
  <th align="left">平台目录</th>
  <th align="left">默认目录</th>
  </tr>
  </thead>
  <tbody>
  <tr class="odd">
  <td align="left"><p>基于 x86</p></td>
  <td align="left"><p>A:\i386</p></td>
  <td align="left"><p>的\\</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p>基于 Itanium</p></td>
  <td align="left"><p>A:\ia64</p></td>
  <td align="left"><p>的\\</p></td>
  </tr>
  <tr class="odd">
  <td align="left"><p>基于 x64</p></td>
  <td align="left"><p>A:\amd64</p></td>
  <td align="left"><p>的\\</p></td>
  </tr>
  </tbody>
  </table>




在跨平台分发磁盘上，Windows 使用平台特定的 *txtsetup.oem* 文件，该文件与运行 Windows 的平台相对应。 如果对应的平台目录包含特定于平台的 *txtsetup.oem* 文件不存在，则 Windows 将在默认目录中使用 *txtsetup.oem* 文件（如果存在）。

Windows 还支持特定于平台的分发磁盘。 平台特定的分发磁盘包含一个特定于平台的 *txtsetup.oem* 文件和相关的驱动程序文件。 *Txtsetup.oem* 文件必须位于其相应的平台目录中，与跨平台分发磁盘或分发磁盘的默认目录中的操作相同。

跨平台分发磁盘或特定于平台的分发磁盘上的给定平台的驱动程序文件必须相对于包含特定于平台的 *txtsetup.oem* 文件的目录。

**提示**  尽管不是必需的，但我们建议始终将 *txtsetup.oem* 文件放在相应的平台目录中。 使用平台目录可消除 Windows 可能尝试使用与运行 Windows 的平台不兼容的 *txtsetup.oem* 文件的可能性。 例如，如果用户在某个平台上尝试使用不包含相应平台目录的分发磁盘进行无人参与的安装，则 Windows 无法确定默认目录中的 *txtsetup.oem* 文件是否与该平台兼容。 如果由于驱动程序与平台不兼容而导致驱动程序无法加载，Windows 将显示一条错误消息并终止无人参与安装。
