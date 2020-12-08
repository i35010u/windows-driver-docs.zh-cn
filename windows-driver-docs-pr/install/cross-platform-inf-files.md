---
title: 跨平台 INF 文件
description: 跨平台 INF 文件
keywords:
- 跨平台 INF 文件 WDK
- INF 文件 WDK 设备安装，跨平台
- 操作系统 WDK，互操作系统 INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1876f0ddaebfdae7fc69099c40f2c57a922d4a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782929"
---
# <a name="cross-platform-inf-files"></a>跨平台 INF 文件


对于跨平台 INF 文件，最简单的策略是为每个平台类型创建单独的 INF 文件，因为这种方法是创建和维护的最简单方法。 有关如何创建特定于平台的 INF 文件的详细信息，请参阅以下主题：

[为基于 x64 的系统创建 INF 文件 (Windows XP 和更高版本) ](inf-file-platform-extensions-and-x64-based-systems.md#creating-inf-files-for-x64-based-systems--windows-xp-and-later-)

[为基于 x86 的系统创建 INF 文件 (Windows 2000 和更高版本) ](inf-file-platform-extensions-and-x86-based-systems.md#creating-inf-files-for-x86-based-systems--windows-2000-and-later-)

如果设备没有特定于操作系统的安装要求，则可以为设备创建一个跨操作系统和跨平台 INF 文件。 例如，如果某个给定平台的操作系统版本中支持某个设备的文件或注册表设置不同，则通常不能为该平台类型创建一个 INF 文件，该文件是所有操作系统版本都支持的。

若要为 Windows 2000 和更高版本的 Windows 创建单个跨操作系统和跨平台 INF 文件，最简单的方法如下所示：

-   对于在基于 Itanium 的系统上安装组件所需的节的名称，请使用 **ntia64** 平台扩展，并使用 **。 ntamd64** 平台扩展用于在基于 x64 的系统上安装组件所需的部分名称。

-   由于 **在** 支持平台扩展的所有部分中， **ntx86** 平台扩展是可选的，因此在基于 x86 的系统上安装组件的部分的名称上不要使用 **nt** 或 **. ntx86** 平台扩展。

若要为 Microsoft Windows 2000 和更高版本的 Windows 创建单个跨操作系统和跨平台 INF 文件，请使用以下过程：

-   对于在基于 Itanium 的系统上安装组件所需的节的名称，请使用 **ntia64** 平台扩展，并使用 **。 ntamd64** 平台扩展用于在基于 x64 的系统上安装组件所需的部分名称。

若要为没有特定于操作系统的要求的设备创建单个跨操作系统和跨平台 INF 文件，支持所有平台类型，并且支持 Windows 2000 及更高版本的 Windows，请执行以下操作：

1. 创建一个有效的 INF 文件，其中包含所有 INF 文件中所需的通用条目，如 [Inf 文件的一般原则](general-guidelines-for-inf-files.md)中所述。

2. 包括一个 "INF **制造商** " 部分，其中包含 *制造商标识符* ，该标识符指定设备的 *型号* 部分名称，以及设备支持的每个平台的平台扩展条目。 例如，以下 "制造商" 部分指定了 *模型* 部分名称 "AbcModelSection" 和平台扩展名 **ntia64** 和 **ntamd64**。  (不指定 **ntx86** 平台扩展。 ) 

   ```cpp
   [Manufacturer]
   ; The manufacturer-identifier for the Abc device.
   %ManufacturerName%=AbcModelSection,ntia64,ntamd64
   ```

3. 包含名称不包含平台扩展的 *模型* 部分。 从 Windows 2000 开始，操作系统为基于 x86 的系统处理此部分。 例如，以下 AbcModelSection 部分为 Abc 设备指定了 "AbcInstallSection" 的 *安装节名称* 。

   ```cpp
   [AbcModelSection]
   %AbcDeviceName%=AbcInstallSection,Abc-hw-id
   ```

4. 包括 ntia64 <em>部分。</em>**.ntia64** Windows Server 2003 SP1 及更高版本需要用于基于 Itanium 的 <em>系统的</em>**ntia64** 部分。 如果存在 <em>Models</em>**Ntia64** 节，Windows SERVER 2003 和 windows XP 还会将此部分用于基于 Itanium 的系统。 例如，以下 AbcModelSection：<strong>ntia64</strong> 部分指定 Abc 设备的 *安装--Name* 为 "AbcInstallSection"。

   ```cpp
   [AbcModelSection.ntia64]
   %AbcDeviceName%=AbcInstallSection.ntia64,Abc-hw-id
   ```

5. 包括 ntamd64 <em>部分。</em>**.ntamd64** Windows Server 2003 SP1 及更高版本需要 <em>一个</em>**ntamd64** 部分，适用于基于 x64 的系统。 如果存在 <em>Models</em>**Ntamd64** 节，Windows SERVER 2003 和 windows XP 还会将此部分用于基于 x64 的系统。 例如，以下 AbcModelSection：<strong>ntamd64</strong> 部分指定 Abc 设备的 *安装--Name* 为 "AbcInstallSection"。

   ```cpp
   AbcModelSectionName.ntamd64
   %AbcDeviceName%=AbcInstallSection.ntamd64,Abc-hw-id
   ```

6. 包含一个 *DDInstall* 节，其名称与不包含平台扩展的 *模型* 部分指定的 *安装节名称* 相同。 例如，AbcModelSection 节指定下面的 AbcInstallSection 节。 Windows 将处理此部分，以在运行 Windows 2000 或更高版本的 Windows 的基于 x86 的系统上安装 Abc 设备。

   ```cpp
   [AbcInstallSection]
   ; Install section entries go here.
   ...
   ```

7. 包括 <em>DDInstall</em>**. ntia64** 节，其名称与 **ntia64** 节 <em>指定的</em>*安装节名称* 相同。 例如，AbcModelSection<strong>. ntia64</strong> 部分指定以下 AbcInstallSection<strong>. ntia64</strong> 节。 Windows 将处理此部分，以便在运行 Windows XP 或更高版本的 Windows 的基于 Itanium 的系统上安装 Abc 设备。

   ```cpp
   [AbcInstallSection.ntia64]
   ; Install section entries go here.
   ...
   ```

8. 包括 <em>DDInstall</em>**. ntamd64** 节，其名称与 **ntamd64** 节 <em>指定的</em>*安装节名称* 相同。 例如，AbcModelSection<strong>. ntamd64</strong> 部分指定以下 AbcInstallSection<strong>. ntamd64</strong> 节。 Windows 将处理此部分，以便在运行 Windows XP 或更高版本的 Windows 的基于 x64 的系统上安装 Abc 设备。

   ```cpp
   [AbcInstallSection.ntamd64]
   ; Install section entries go here.
   ...
   ```

9. 包括基于 x86 的安装所需的其他特定于设备的部分。 请勿在这些部分的名称中包含 **ntx86** 平台扩展。 默认情况下，Windows 将处理这些部分，以在运行 Windows 2000 或更高版本的 Windows 的基于 x86 的系统上安装设备。

10. 包括运行 Windows XP 或更高版本的 Windows 的基于 Itanium 的系统所需的其他特定于设备的部分。 对这些节名称包含 **ntia64** 扩展名。

11. 包括运行 Windows XP 或更高版本的 Windows 的基于 x64 的系统所需的其他特定于设备的部分。 对这些节名称包含 **ntamd64** 扩展名。

有关 INF 文件部分和指令的详细信息，请参阅 [Inf 部分摘要](summary-of-inf-sections.md) 和 [inf 指令摘要](summary-of-inf-directives.md)。

 

 





