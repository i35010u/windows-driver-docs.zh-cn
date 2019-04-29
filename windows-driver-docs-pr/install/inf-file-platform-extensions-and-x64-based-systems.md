---
title: INF 文件平台扩展和基于 x64 的系统
description: INF 文件平台扩展和基于 x64 的系统
ms.assetid: 062c58f7-3519-4835-9597-ab6be5ff5fe8
keywords:
- x64 INF 文件平台扩展 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ac311ac10eb3a2188309d0382392bd3a7401ef6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391996"
---
# <a name="inf-file-platform-extensions-and-x64-based-systems"></a>INF 文件平台扩展和基于 x64 的系统


### <a href="" id="platform-extensions-and-x64-based-systems--windows-xp-and-later-"></a> 平台扩展和基于 x64 的系统 (Windows XP 及更高版本)

Windows Server 2003 Service Pack 1 (SP1) 及更高版本， **.ntamd64**上需要平台扩展[ **INF 模型部分**](inf-models-section.md)。 **.Ntamd64**或 **.nt**平台扩展名的所有支持平台扩展的其他部分是可选的。

对于支持可选的平台扩展的部分，Windows 将选择哪个部分进行处理，按如下所示：

1. Windows 将检查<em>节名称</em>**.ntamd64**部分和，如果存在，对其进行处理。 检查 Windows **.ntamd64**扩展正在处理的 INF 文件中，并在任何包含的 INF 文件 (即，任何 INF 文件附带**Include**条目)。

2. 如果<em>节名称</em>**.ntamd64**节不存在，Windows 将检查<em>节名称</em>**.nt**中 INF 文件或任何部分包含的 INF 文件。 如果存在，Windows 将处理<em>节名称</em>**.nt**部分。

3. 如果<em>节名称</em>**.nt**节不存在，Windows 处理*节名称*部分，其中不包含平台扩展。

### <a href="" id="testing-installation-on-x64-based-systems--windows-server-2003-sp1-and"></a> 测试基于 x64 的系统上安装 (Windows Server 2003 SP1 及更高版本)

仅出于测试目的，此要求， [ **INF 模型部分**](inf-models-section.md)名称包含 **.ntamd64**扩展可被禁止。 若要禁止显示此要求，请创建以下注册表值项子项下的**HKLM\\软件\\Microsoft\\Windows\\CurrentVersion\\设置**并将此值项设置为一个：

```ini
DisableDecoratedModelsRequirement:REG_DWORD
```

设置后**DisableDecoratedModelsRequirement**值到一个项目，重新启动系统，然后安装该设备。

若要还原的平台扩展要求，请删除**DisableDecoratedModelsRequirement**值项目或将其设置为零，，然后重新启动系统。

### <a href="" id="creating-inf-files-for-x64-based-systems--windows-xp-and-later-"></a> 创建基于 x64 的系统的 INF 文件 (Windows XP 及更高版本)

一般情况下，不能使用单个的 INF 文件，用于区分根据操作系统版本的设备安装。 例如，如果文件或支持设备的注册表设置的基于 x64 的操作系统版本之间存在差异，必须创建每个版本的特定于操作系统的 INF 文件。

但是，如果设备不需要特定于操作系统的安装，您可以创建单个跨操作系统的系统 INF 文件的基于 x64 的系统的运行 Windows XP 及更高版本。

因为 Windows Server 2003 SP1 和更高版本需要 **.ntamd64**上的平台扩展[ **INF 模型部分**](inf-models-section.md)名称，但不是需要此扩展在其他部分名称，最简单的方法来创建和维护基于 x64 的系统跨操作系统的系统 INF 文件是包含 **.ntamd64**上的名称仅扩展*模型*部分。

若要创建此类跨操作系统系统 INF 文件，请执行以下操作：

1. 创建有效的 INF 文件包含所有的 INF 文件中所需的通用项，如中所述[INF 文件的一般准则](general-guidelines-for-inf-files.md)。

2. 包括 INF**制造商**包含的部分*制造商标识符*，它指定[ **INF 模型部分**](inf-models-section.md)名称对于设备，并指定 **.ntamd64**平台扩展。 例如，以下**制造商**部分指定 INF*模型*Abc 设备的"AbcModelSection"部分名称， **.ntamd64**平台扩展。

   ```ini
   [Manufacturer]
   ; The manufacturer-identifier for the Abc device.
   %ManufacturerName%=AbcModelSection,ntamd64
   ```

3. 包括<em>模型</em>**.ntamd64**其名称与匹配的部分*模型*由指定的节名称*制造商标识符*中**制造商**部分。 例如，以下 AbcModelSection<strong>.ntamd64</strong> Abc 设备包括部分*设备描述*，它指定*安装的部分名称*的"AbcInstallSection。"

   ```ini
   [AbcModelSection.ntamd64]
   %AbcDeviceName%=AbcInstallSection,Abc-hw-id
   ```

4. 包括*DDInstall*其名称与匹配的部分*安装部分名称*由指定*模型*部分。 例如，*设备描述*AbcModelSection 中部分指定以下 AbcInstallSection 部分的 Abc 设备。

   ```ini
   [AbcInstallSection]
   ; Install section entries go here.
   ...
   ```

5. 包括的所需安装该设备，但不是包括其他特定于设备的节 **.ntamd64**平台上的这些部分名称的扩展。 有关 INF 文件的部分和指令的详细信息，请参阅[INF 部分摘要](summary-of-inf-sections.md)并[INF 指令摘要](summary-of-inf-directives.md)。

有关如何创建一个单跨操作系统系统，INF 用于所有平台类型的信息，请参阅[跨平台 INF 文件](cross-platform-inf-files.md)。

 

 





