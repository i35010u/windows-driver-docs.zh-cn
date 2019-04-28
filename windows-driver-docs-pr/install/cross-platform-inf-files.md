---
title: 跨平台 INF 文件
description: 跨平台 INF 文件
ms.assetid: 5f7e80d2-b8b5-4ce9-9e70-cacc51223deb
keywords:
- 跨平台 INF 文件 WDK
- INF 文件 WDK 设备安装，跨平台
- 操作系统 WDK，跨操作系统系统 INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee9118a88cd58d5a3219f906d879d34da5175083
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352078"
---
# <a name="cross-platform-inf-files"></a>跨平台 INF 文件


跨平台 INF 文件的最简单的策略是创建单独的 INF 文件为每个平台类型，因为这种方法是最简单的方法来创建和维护。 有关如何创建特定于平台的 INF 文件的详细信息，请参阅以下主题：

[创建基于 x64 的系统的 INF 文件 (Windows XP 及更高版本)](inf-file-platform-extensions-and-x64-based-systems.md#creating-inf-files-for-x64-based-systems--windows-xp-and-later-)

[创建基于 x86 的系统 (Windows 2000 及更高版本) 的 INF 文件](inf-file-platform-extensions-and-x86-based-systems.md#creating-inf-files-for-x86-based-systems--windows-2000-and-later-)

如果设备不具有特定于操作系统的安装要求，可以创建单个跨操作系统和设备的跨平台 INF 文件。 例如，如果给定平台的操作系统版本之间存在差异的文件或注册表设置的支持的设备，一般情况下，不能请创建一个 INF 文件由所有操作系统版本支持该平台类型。

若要创建单个跨操作系统和 Windows 2000 和更高版本的 Windows 的跨平台 INF 文件，最简单的方法如下所示：

-   使用 **.ntia64**平台上的基于 Itanium 的系统上安装组件，并使用所需的部分名称的扩展 **.ntamd64**平台扩展上的各节的名称所需组件安装在基于 x64 的系统上。

-   因为 **.nt**并 **.ntx86**平台扩展支持的平台扩展的所有部分都是可选，则不要使用 **.nt**或 **.ntx86**平台扩展上的组件安装在基于 x86 的系统的部分的名称。

若要创建单个跨操作系统和 Microsoft Windows 2000 和更高版本的 Windows 的跨平台 INF 文件，请使用以下过程：

-   使用 **.ntia64**平台上的基于 Itanium 的系统上安装组件，并使用所需的部分名称的扩展 **.ntamd64**平台扩展上的各节的名称所需组件安装在基于 x64 的系统上。

创建单个跨操作系统和跨平台 INF 文件不具有特定于操作系统的要求的设备支持所有平台类型，并都支持 Windows 2000 和更高版本的 Windows，执行以下操作：

1. 创建有效的 INF 文件包含所有的 INF 文件中所需的通用项，如中所述[INF 文件的一般准则](general-guidelines-for-inf-files.md)。

2. 包括 INF**制造商**包含的部分*制造商标识符*，它指定*模型*设备和平台扩展条目的节名称为每个设备支持的平台。 例如，以下的制造商部分指定*模型*"AbcModelSection"和平台扩展的节名称 **.ntia64**并 **.ntamd64**。 (未指定 **.ntx86**平台扩展。)

   ```cpp
   [Manufacturer]
   ; The manufacturer-identifier for the Abc device.
   %ManufacturerName%=AbcModelSection,ntia64,ntamd64
   ```

3. 包括*模型*部分其名称不包含平台扩展。 操作系统从 Windows 2000 开始，处理此部分针对基于 x86 的系统。 例如，以下 AbcModelSection 部分指定*安装的部分名称*的"AbcInstallSection"Abc 设备。

   ```cpp
   [AbcModelSection]
   %AbcDeviceName%=AbcInstallSection,Abc-hw-id
   ```

4. 包括<em>模型</em>**.ntia64**部分。 Windows Server 2003 SP1 和更高版本需要<em>模型</em>**.ntia64**用于基于 Itanium 的系统部分。 如果<em>模型</em>**.ntia64**部分存在，则 Windows Server 2003 和 Windows XP 还使用此部分用于基于 Itanium 的系统。 例如，以下 AbcModelSection<strong>.ntia64</strong>部分指定*安装部分名称*的"AbcInstallSection.ntia64"Abc 设备。

   ```cpp
   [AbcModelSection.ntia64]
   %AbcDeviceName%=AbcInstallSection.ntia64,Abc-hw-id
   ```

5. 包括<em>模型</em>**.ntamd64**部分。 Windows Server 2003 SP1 和更高版本需要<em>模型</em>**.ntamd64**针对基于 x64 的系统部分。 如果<em>模型</em>**.ntamd64**部分存在，则 Windows Server 2003 和 Windows XP 还使用此部分用于基于 x64 的系统。 例如，以下 AbcModelSection<strong>.ntamd64</strong>部分指定*安装部分名称*的"AbcInstallSection.ntamd64"Abc 设备。

   ```cpp
   AbcModelSectionName.ntamd64
   %AbcDeviceName%=AbcInstallSection.ntamd64,Abc-hw-id
   ```

6. 包括*DDInstall*其名称是相同的部分作为*安装部分名称*由指定*模型*部分，其中不包含平台扩展。 例如，AbcModelSection 部分指定以下 AbcInstallSection 部分。 Windows 处理此部分以在运行 Windows 2000 或更高版本的 Windows 的基于 x86 的系统上安装 Abc 设备。

   ```cpp
   [AbcInstallSection]
   ; Install section entries go here.
   ...
   ```

7. 包括<em>DDInstall</em>**.ntia64**其名称是相同的部分作为*安装的部分名称*由指定<em>模型</em>**.ntia64**部分。 例如，AbcModelSection<strong>.ntia64</strong>部分指定以下 AbcInstallSection<strong>.ntia64</strong>部分。 Windows 处理此部分以在运行 Windows XP 或更高版本的 Windows 的基于 Itanium 的系统上安装 Abc 设备。

   ```cpp
   [AbcInstallSection.ntia64]
   ; Install section entries go here.
   ...
   ```

8. 包括<em>DDInstall</em>**.ntamd64**其名称是相同的部分作为*安装的部分名称*由指定<em>模型</em>**.ntamd64**部分。 例如，AbcModelSection<strong>.ntamd64</strong>部分指定以下 AbcInstallSection<strong>.ntamd64</strong>部分。 Windows 处理此部分以在运行 Windows XP 或更高版本的 Windows 的基于 x64 的系统上安装 Abc 设备。

   ```cpp
   [AbcInstallSection.ntamd64]
   ; Install section entries go here.
   ...
   ```

9. 包括基于 x86 的安装所需的其他特定于设备的部分。 不包括 **.ntx86**平台扩展上的这些部分的名称。 默认情况下运行 Windows 2000 或更高版本的 Windows 的基于 x86 的系统上安装该设备，Windows 处理这些部分。

10. 包括所需的运行 Windows XP 或更高版本的 Windows 的基于 Itanium 的系统的其他特定于设备的部分。 包括 **.ntia64**上这些部分名称的扩展。

11. 包括所需的运行 Windows XP 或更高版本的 Windows 的基于 x64 的系统的其他特定于设备的部分。 包括 **.ntamd64**上这些部分名称的扩展。

有关 INF 文件的部分和指令的详细信息，请参阅[INF 部分摘要](summary-of-inf-sections.md)并[INF 指令摘要](summary-of-inf-directives.md)。

 

 





