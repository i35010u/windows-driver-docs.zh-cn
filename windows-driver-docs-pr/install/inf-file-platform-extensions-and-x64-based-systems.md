---
title: INF 文件平台扩展和基于 x64 的系统
description: INF 文件平台扩展和基于 x64 的系统
ms.assetid: 062c58f7-3519-4835-9597-ab6be5ff5fe8
keywords:
- x64 INF 文件平台扩展 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ac311ac10eb3a2188309d0382392bd3a7401ef6
ms.sourcegitcommit: e1cfed28850a8208ea27e7a6a336de88c48e9948
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78402506"
---
# <a name="inf-file-platform-extensions-and-x64-based-systems"></a>INF 文件平台扩展和基于 x64 的系统


### <a href="" id="platform-extensions-and-x64-based-systems--windows-xp-and-later-"></a>平台扩展和基于 x64 的系统（Windows XP 及更高版本）

在 Windows Server 2003 Service Pack 1 （SP1）和更高版本中， [**INF 型号部分**](inf-models-section.md)需要**ntamd64**平台扩展。 对于支持平台扩展的所有其他部分， **ntamd64**或**nt**平台扩展是可选的。

对于支持可选平台扩展的部分，Windows 会选择要处理的部分，如下所示：

1. Windows 将检查<em>节名称</em> **. ntamd64**部分，如果存在，则对其进行处理。 Windows 将检查正在处理的 INF 文件和任何包含的 INF 文件中的**ntamd64**扩展（即包含**包含**在包含项中的任何 inf 文件）。

2. 如果<em>节名称</em>**ntamd64**部分不存在，则 Windows 将检查 inf 文件或任何包含的 inf 文件中的<em>部分名称</em>**nt 部分。** 如果存在，则 Windows 将处理<em>节名称</em>**nt**部分。

3. 如果<em>节名</em>**nt**部分不存在，则 Windows 将处理不包含平台扩展的*节名称*节。

### <a href="" id="testing-installation-on-x64-based-systems--windows-server-2003-sp1-and"></a>在基于 x64 的系统上进行安装测试（Windows Server 2003 SP1 及更高版本）

仅出于测试目的，要求[**INF 型号部分**](inf-models-section.md)名称包含**ntamd64 扩展名。** 若要取消此要求，请在 **\\Software\\Microsoft\\Windows\\CurrentVersion\\安装程序**下的子项 HKLM 下创建以下注册表值项，并将此值项设置为一：

```ini
DisableDecoratedModelsRequirement:REG_DWORD
```

将**DisableDecoratedModelsRequirement**值项设置为 one 后，重新启动系统，然后安装该设备。

若要还原平台扩展要求，请删除**DisableDecoratedModelsRequirement**值项或将其设置为零，然后重新启动系统。

### <a href="" id="creating-inf-files-for-x64-based-systems--windows-xp-and-later-"></a>为基于 x64 的系统创建 INF 文件（Windows XP 及更高版本）

通常，你不能使用单个 INF 文件来区分基于操作系统版本的设备安装。 例如，如果支持设备的文件或注册表设置在基于 x64 的操作系统版本之间不同，则必须为每个版本创建特定于操作系统的 INF 文件。

但是，如果设备不需要特定于操作系统的安装，则可以为运行 Windows XP 和更高版本的基于 x64 的系统创建单个跨操作系统 INF 文件。

由于 Windows Server 2003 SP1 和更高版本在[**INF 型号部分**](inf-models-section.md)名称上需要**ntamd64**平台扩展，但不需要在其他部分名称上使用此扩展，因此，创建和维护基于 x64 的系统的跨操作系统 INF 文件的最简单方法是仅在*模型*的名称部分中包括**ntamd64**扩展。

若要创建此类跨操作系统 INF 文件，请执行以下操作：

1. 创建一个有效的 INF 文件，其中包含所有 INF 文件中所需的通用条目，如[Inf 文件的一般原则](general-guidelines-for-inf-files.md)中所述。

2. 包括一个 INF**制造商**部分，其中包含*制造商标识符*，该标识符指定设备的[**INF 型号部分**](inf-models-section.md)名称并指定**ntamd64**平台扩展。 例如，以下**制造商**部分为 Abc 设备指定了 "AbcModelSection" 的 INF*型号*部分名称和 **. ntamd64**平台扩展。

   ```ini
   [Manufacturer]
   ; The manufacturer-identifier for the Abc device.
   %ManufacturerName%=AbcModelSection,ntamd64
   ```

3. 包括一个**ntamd64**节，其名称与**制造商部分中**的*制造商标识符*指定的*模型*部分名称匹配。 例如，Abc 设备的以下 AbcModelSection<strong>ntamd64</strong>部分包含*设备说明*，用于指定 "AbcInstallSection" 的*安装节名称*。

   ```ini
   [AbcModelSection.ntamd64]
   %AbcDeviceName%=AbcInstallSection,Abc-hw-id
   ```

4. 包括名称与 "*模型*" 部分指定的*安装节名称*匹配的*DDInstall*节。 例如，AbcModelSection 节中的*设备说明*为 Abc 设备指定以下 AbcInstallSection 部分。

   ```ini
   [AbcInstallSection]
   ; Install section entries go here.
   ...
   ```

5. 包括安装设备所需的其他特定于设备的部分，但不包括这些部分名称的**ntamd64**平台扩展。 有关 INF 文件部分和指令的详细信息，请参阅[Inf 部分摘要](summary-of-inf-sections.md)和[inf 指令摘要](summary-of-inf-directives.md)。

有关如何为所有平台类型创建单个跨操作系统 INF 的信息，请参阅[跨平台 Inf 文件](cross-platform-inf-files.md)。

 

 





