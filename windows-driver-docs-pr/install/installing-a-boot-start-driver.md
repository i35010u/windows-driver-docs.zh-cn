---
title: 安装引导启动驱动程序
description: 安装引导启动驱动程序
ms.assetid: 0b93233b-266c-4d2e-a5d8-01d2d477dd13
keywords:
- 设备安装程序 WDK 设备安装，启动驱动程序
- 设备安装 WDK，启动驱动程序
- 安装 WDK 的设备，请启动驱动程序
- 启动驱动程序 WDK 设备安装
- 启动驱动程序分发磁盘 WDK 设备安装
- 分发磁盘 WDK
- 特定于平台的分发磁盘 WDK
- 跨平台分发磁盘 WDK
- 供应商提供的启动驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 492fb91aaa4ef4f2ef9958bfea720cfbffc29cd8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357506"
---
# <a name="installing-a-boot-start-driver"></a>安装引导启动驱动程序





一个*引导启动驱动程序*是必须安装，以启动 Microsoft Windows 操作系统的设备的驱动程序。 大多数引导启动驱动程序是包含"中现成"的 Windows，并且 Windows 会自动将这些引导启动驱动程序安装在 Windows 安装的文本模式安装阶段。 如果设备的引导启动驱动程序不包含"中现成"的 Windows，用户可以在文本模式下安装期间安装设备的其他供应商提供引导启动驱动程序。

若要安装需要用来启动 Windows，但其驱动程序不包括与操作系统的设备，用户必须执行以下操作：

1.  安装设备硬件并在计算机上打开。

2.  开始 Windows 安装 （运行 Windows 安装程序）。 在文本模式阶段 （在安装开头） 安装的 Windows 将显示一条消息，指示，你可以按特定 **F * * * n*密钥以安装引导启动驱动程序。

3.  当 Windows 显示此消息时，请按指定 **F * * * n*键安装引导启动驱动程序，然后插入[引导启动驱动程序分发磁盘](#boot-start-driver-distribution-disk)。

**请注意**此过程说明了如何安装未包含"中现成"的 Windows 驱动程序。 不使用此过程用于替换或更新包含在 Windows 的驱动程序。 相反，等待，直到 Windows 启动并使用设备管理器执行在设备上的"更新驱动程序"操作。



如果 Windows 无法启动，可以显示某些错误消息，指示引导启动驱动程序丢失。 下表描述了多条错误消息和可能的原因。

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
<td align="left"><p>无法访问启动设备</p></td>
<td align="left"><p>启动磁盘是需要一个未包括在 Windows 的驱动程序的第三方大容量存储设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p>安装程序无法确定计算机类型</p></td>
<td align="left"><p>新的 HAL 驱动程序是必需的。 大多数计算机上不会出现此错误，但在高端服务器可能会出现。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>在您的计算机，安装程序找不到任何硬盘驱动器</p></td>
<td align="left"><p>未加载的硬盘驱动器的所需的启动设备驱动程序。</p></td>
</tr>
</tbody>
</table>



### <a href="" id="boot-start-driver-distribution-disk"></a> 引导启动驱动程序分发磁盘

一个*引导启动驱动程序分发磁盘*是一个媒介，如软盘或 USB 闪存驱动器，其中包含*TxtSetup.oem*文件和相关的驱动程序文件。 *TxtSetup.oem*文件是包含的文件将复制到系统中，在分布磁盘上的列表和注册表项和值将创建一系列的硬件组件列表的文本文件。 一个示例*TxtSetup.oem*文件下提供了使用 Windows Driver Kit (WDK) 中， \\WDK 的 src 目录。 有关详细信息的内容*TxtSetup.oem*文件，请参阅[TxtSetup.oem 文件格式](https://msdn.microsoft.com/library/windows/hardware/ff553509)。

以下要求和建议适用于特定于平台和跨平台分发版磁盘：

- 特定于平台的分发磁盘 (Windows Server 2003 及更早版本)

  Windows 驱动程序支持的每个平台需要特定于平台的通讯组磁盘。 特定于平台的分发磁盘包含一个*TxtSetup.oem*文件和相关的驱动程序文件。 *TxtSetup.oem*文件必须位于分发磁盘的根目录中。

- 跨平台和特定于平台的分发磁盘 （Windows Server 2003 Service Pack 1 (SP1) 和更高版本）

  Windows 支持包含两个或多个平台特定的跨平台分发磁盘*TxtSetup.oem*文件和相关的驱动程序文件。

  若要区分平台的跨平台分发磁盘上，使用下表中列出的平台目录。

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
  <td align="left"><p>基于 x86 的</p></td>
  <td align="left"><p>A:\i386</p></td>
  <td align="left"><p>答：\\</p></td>
  </tr>
  <tr class="even">
  <td align="left"><p>基于 Itanium 的</p></td>
  <td align="left"><p>A:\ia64</p></td>
  <td align="left"><p>答：\\</p></td>
  </tr>
  <tr class="odd">
  <td align="left"><p>基于 x64</p></td>
  <td align="left"><p>A:\amd64</p></td>
  <td align="left"><p>答：\\</p></td>
  </tr>
  </tbody>
  </table>




在跨平台分发磁盘上，Windows 将使用特定于平台的*TxtSetup.oem*位于对应于在其运行 Windows 的平台的平台目录中的文件。 如果包含平台特定的相应平台目录*TxtSetup.oem*文件不存在，Windows 将使用*TxtSetup.oem*文件在默认目录中，如果不存在。

Windows 还支持特定于平台的通讯组磁盘。 特定于平台的分发磁盘包含一个平台专属*TxtSetup.oem*文件和相关的驱动程序文件。 *TxtSetup.oem*文件必须位于其相应的平台目录中，就这样做的跨平台分发磁盘或分发磁盘在默认目录中。

驱动程序文件给定平台的跨平台分发磁盘上或特定于平台的分发磁盘上必须位于相对于包含特定于平台的目录*TxtSetup.oem*文件。

**提示**尽管没有要求，我们建议*TxtSetup.oem*文件始终放置在相应的平台目录中。 使用平台目录可消除 Windows 可能会尝试使用的可能性*TxtSetup.oem*与 Windows 运行时所在的平台不兼容的文件。 例如，如果用户尝试使用分发磁盘不包含相应的平台目录平台上的无人参与的安装，Windows 无法确定是否*TxtSetup.oem*在默认的文件目录是与平台兼容。 如果驱动程序无法加载，因为该驱动程序的平台不兼容，Windows 将显示一条错误消息，并终止无人参与的安装。












