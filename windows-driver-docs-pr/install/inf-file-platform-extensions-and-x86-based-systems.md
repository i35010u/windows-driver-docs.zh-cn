---
title: INF 文件平台扩展和基于 x86 的系统
description: INF 文件平台扩展和基于 x86 的系统
ms.assetid: d0e1c6ba-32c4-413d-b0d9-620e3617a62b
keywords:
- x86 INF 文件平台扩展 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b100a09c2f2c2794963404030e95260e9727d6da
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79243030"
---
# <a name="inf-file-platform-extensions-and-x86-based-systems"></a>INF 文件平台扩展和基于 x86 的系统


下表总结了对运行 Windows 2000 和更高版本 Windows 的基于 x86 的系统的平台扩展的 Windows 支持。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">平台扩展</th>
<th align="left">平台扩展支持（Windows 2000 及更高版本）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>.ntamd64</strong></p></td>
<td align="left"><p>不受支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.ntia64</strong></p></td>
<td align="left"><p>不受支持。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>.ntarm</strong></p></td>
<td align="left"><p>不受支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.ntarm64</strong></p></td>
<td align="left"><p>不受支持。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>.ntx86</strong></p></td>
<td align="left"><p>在支持扩展的节中为可选。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>。 nt</strong></p></td>
<td align="left"><p>在支持扩展的节中为可选。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>（无平台扩展）</p></td>
<td align="left"><p>默认情况下，在所有部分都受支持。</p></td>
</tr>
</tbody>
</table>

 

有关如何在基于 x86 的系统上使用平台扩展的详细信息，请参阅以下部分：

[平台扩展和基于 x86 的系统（Windows 2000 及更高版本）](#platform-extensions-and-x86-based-systems--windows-2000-and-later-)

[为基于 x86 的系统创建 INF 文件（Windows 2000 及更高版本）](#creating-inf-files-for-x86-based-systems--windows-2000-and-later-)

### <a href="" id="platform-extensions-and-x86-based-systems--windows-2000-and-later-"></a>平台扩展和基于 x86 的系统

Windows XP 和更高版本的 Windows 支持在*模型*中使用可选的**nt**或 **. ntx86**平台扩展，以及支持平台扩展的其他部分的名称。

Windows 2000 不支持[**INF*型号*部分**](inf-models-section.md)名称上的平台扩展，但在支持平台扩展的其他部分的名称上支持可选的**nt**或**ntx86**平台扩展。

对于支持可选平台扩展的部分，Windows 会选择要处理的部分，如下所示：

1. Windows 将检查<em>节名称</em> **. ntx86**部分，如果存在，则对其进行处理。 Windows 将检查正在处理的 INF 文件和任何包含的 INF 文件中的**ntx86**扩展（即包含**包含**在包含项中的任何 inf 文件）。

2. 如果<em>节名称</em>**ntx86**部分不存在，则 Windows 将检查 inf 文件或任何包含的 inf 文件中的<em>部分名称</em>**nt 部分。** 如果存在，则 Windows 将处理<em>节名称</em>**nt**部分。

3. 如果<em>节名</em>**nt**部分不存在，则 Windows 将处理不包含平台扩展的*节名称*节。

### <a href="" id="creating-inf-files-for-x86-based-systems--windows-2000-and-later-"></a>为基于 x86 的系统创建 INF 文件

通常，你不能使用单个 INF 文件来区分基于操作系统版本的设备安装。 例如，如果支持设备的文件或注册表设置在基于 x86 的操作系统版本之间不同，则必须为每个版本创建特定于操作系统的 INF 文件。

但是，如果设备不需要特定于操作系统的安装，则可以为运行 Windows 2000 和更高版本 Windows 的基于 x86 的系统创建单个跨操作系统 INF 文件。

由于**ntx86**平台扩展是可选的，因此，最简单的方法是创建并维护基于 x86 的系统的跨操作系统 INF 文件，而不是在部分名称上使用平台**扩展。**

若要为运行 Windows 2000 和更高版本 Windows 的基于 x86 的系统创建单个跨操作系统 INF 文件，请执行以下操作：

1.  创建一个有效的 INF 文件，其中包含所有 INF 文件中所需的通用条目，如[Inf 文件的一般原则](general-guidelines-for-inf-files.md)中所述。

2.  包括一个 INF**制造商**部分，其中包含*制造商标识符*，该标识符指定设备的*型号*部分名称，但不指定可选的**nt**或 **. ntx86**平台扩展。 例如，以下**制造商**部分为 Abc 设备指定了 "AbcModelSection"*模型*部分名称。

    ```ini
    [Manufacturer]
    ; The manufacturer-identifier for the Abc device.
    %ManufacturerName%=AbcModelSection
    ```

3.  包括名称与 "**制造商**" 部分中*制造商标识符*指定的 "*模型*" 部分名称匹配的*模型*部分。 例如，Abc 设备的以下 AbcModelSection 部分包含*设备说明*，该说明指定了 "AbcInstallSection" 的*安装节名称*。

    ```ini
    [AbcModelSection]
    %AbcDeviceName%=AbcInstallSection,Abc-hw-id
    ```

4.  包括名称与 "*模型*" 部分指定的*安装节名称*匹配的*DDInstall*节。 例如，"AbcModelSection" 部分中的 "*设备说明*" 为 Abc 设备指定以下 AbcInstallSection 部分。 Windows 将处理此部分，以在运行 Windows 2000 和更高版本的 Windows 的基于 x86 的系统上安装 Abc 设备。

    ```ini
    [AbcInstallSection]
    ; Install section entries go here.
    ...
    ```

5.  包括安装设备所需的其他特定于设备的部分，但在这些部分的名称上不包括**nt**或**ntx86**平台扩展。 Windows 将处理这些部分，以在运行 Windows 2000 和更高版本的 Windows 的基于 x86 的系统上安装 Abc 设备。

有关 INF 文件部分和指令的详细信息，请参阅[Inf 部分摘要](summary-of-inf-sections.md)和[inf 指令摘要](summary-of-inf-directives.md)。

有关如何为所有平台类型创建单个跨平台 INF 文件的信息，请参阅[跨平台 Inf 文件](cross-platform-inf-files.md)。

 

 





