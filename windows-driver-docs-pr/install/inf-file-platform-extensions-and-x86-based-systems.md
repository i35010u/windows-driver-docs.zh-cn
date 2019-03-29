---
title: INF 文件平台扩展和基于 x86 的系统
description: INF 文件平台扩展和基于 x86 的系统
ms.assetid: d0e1c6ba-32c4-413d-b0d9-620e3617a62b
keywords:
- x86 INF 文件平台扩展 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b100a09c2f2c2794963404030e95260e9727d6da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567546"
---
# <a name="inf-file-platform-extensions-and-x86-based-systems"></a>INF 文件平台扩展和基于 x86 的系统


下表总结了运行 Windows 2000 和更高版本的 Windows 的基于 x86 的系统的平台扩展的 Windows 支持。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">平台扩展</th>
<th align="left">平台扩展支持 (Windows 2000 及更高版本)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>.ntamd64</strong></p></td>
<td align="left"><p>不支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.ntia64</strong></p></td>
<td align="left"><p>不支持。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>.ntarm</strong></p></td>
<td align="left"><p>不支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.ntarm64</strong></p></td>
<td align="left"><p>不支持。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>.ntx86</strong></p></td>
<td align="left"><p>在支持扩展的部分可选。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.nt</strong></p></td>
<td align="left"><p>在支持扩展的部分可选。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>（无扩展名平台）</p></td>
<td align="left"><p>默认情况下，在所有部分支持。</p></td>
</tr>
</tbody>
</table>

 

有关如何使用基于 x86 的系统使用平台扩展的详细信息，请参阅以下各节：

[平台扩展和基于 x86 的系统 (Windows 2000 及更高版本)](#platform-extensions-and-x86-based-systems--windows-2000-and-later-)

[创建基于 x86 的系统 (Windows 2000 及更高版本) 的 INF 文件](#creating-inf-files-for-x86-based-systems--windows-2000-and-later-)

### <a href="" id="platform-extensions-and-x86-based-systems--windows-2000-and-later-"></a> 平台扩展和基于 x86 的系统

Windows XP 和更高版本的 Windows 支持的可选 **.nt**或 **.ntx86**上的平台扩展*模型*部分名称和支持的其他部分的名称平台扩展。

Windows 2000 不支持上的平台扩展[ **INF*模型*部分**](inf-models-section.md)名称，但支持可选 **.nt**或 **.ntx86**平台扩展上的支持平台扩展的其他部分的名称。

对于支持可选的平台扩展的部分，Windows 将选择哪个部分进行处理，按如下所示：

1. Windows 将检查<em>节名称</em>**.ntx86**部分和，如果存在，对其进行处理。 检查 Windows **.ntx86**扩展正在处理的 INF 文件中，并在任何包含的 INF 文件 (即，任何 INF 文件附带**Include**条目)。

2. 如果<em>节名称</em>**.ntx86**节不存在，Windows 将检查<em>节名称</em>**.nt**中 INF 文件或任何部分包含的 INF 文件。 如果存在，Windows 将处理<em>节名称</em>**.nt**部分。

3. 如果<em>节名称</em>**.nt**节不存在，Windows 处理*节名称*部分，其中不包含平台扩展。

### <a href="" id="creating-inf-files-for-x86-based-systems--windows-2000-and-later-"></a> 创建基于 x86 的系统的 INF 文件

一般情况下，不能使用单个的 INF 文件，用于区分根据操作系统版本的设备安装。 例如，如果文件或支持设备的注册表设置的基于 x86 的操作系统版本之间存在差异，必须创建每个版本的特定于操作系统的 INF 文件。

但是，如果设备不需要特定于操作系统的安装，您可以创建运行 Windows 2000 和更高版本的 Windows 的基于 x86 的系统的单跨操作系统系统 INF 文件。

因为 **.nt**并 **.ntx86**是可选的平台扩展、 创建和维护针对基于 x86 的系统跨操作系统的系统 INF 文件的最简单方法是不在使用平台扩展节名称。

若要创建运行 Windows 2000 和更高版本的 Windows 的基于 x86 的系统的单跨操作系统的系统 INF 文件，请执行以下操作：

1.  创建有效的 INF 文件包含所有的 INF 文件中所需的通用项，如中所述[INF 文件的一般准则](general-guidelines-for-inf-files.md)。

2.  包括 INF**制造商**包含的部分*制造商标识符*，它指定*模型*节名称对于设备，但未指定可选 **.nt**或 **.ntx86**平台扩展。 例如，以下**制造商**部分指定*模型*Abc 设备的"AbcModelSection"部分名称。

    ```ini
    [Manufacturer]
    ; The manufacturer-identifier for the Abc device.
    %ManufacturerName%=AbcModelSection
    ```

3.  包括*模型*其名称与匹配的部分*模型*由指定的节名称*制造商标识符*中**制造商**部分。 例如，Abc 设备的以下 AbcModelSection 部分包括*设备描述*，它指定*安装部分名称*的"AbcInstallSection。"

    ```ini
    [AbcModelSection]
    %AbcDeviceName%=AbcInstallSection,Abc-hw-id
    ```

4.  包括*DDInstall*其名称与匹配的部分*安装部分名称*由指定*模型*部分。 例如，*设备描述*AbcModelSection 中部分指定以下 AbcInstallSection 部分的 Abc 设备。 Windows 处理此部分以在运行 Windows 2000 和更高版本的 Windows 的基于 x86 的系统上安装 Abc 设备。

    ```ini
    [AbcInstallSection]
    ; Install section entries go here.
    ...
    ```

5.  包括的所需安装该设备，但不是包括其他特定于设备的节 **.nt**或 **.ntx86**平台扩展上的这些部分的名称。 Windows 处理以下各节，在运行 Windows 2000 和更高版本的 Windows 的基于 x86 的系统上安装 Abc 设备。

有关 INF 文件的部分和指令的详细信息，请参阅[INF 部分摘要](summary-of-inf-sections.md)并[INF 指令摘要](summary-of-inf-directives.md)。

有关如何创建所有平台类型的单个跨平台 INF 文件的信息，请参阅[跨平台 INF 文件](cross-platform-inf-files.md)。

 

 





