---
title: INF 文件的源媒体
description: INF 文件的源媒体
ms.assetid: b8bb7115-acac-4364-a205-16816c52fdb0
keywords:
- INF 文件 WDK 设备安装，源媒体
- 媒体 WDK INF 文件
- 源媒体 WDK INF 文件
- 多功能设备 WDK INF 文件
- 修饰的 INF WDK
- INF 文件 WDK 设备安装，单独传送
- 传送 INF 文件 WDK
- 单独传送 INF 文件 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b66da54bc9c78a39e7d99f2106a4e7de69f1dfa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348607"
---
# <a name="source-media-for-inf-files"></a>INF 文件的源媒体





应使用来指定设备文件的源媒体的方法取决于是否您的 INF 文件分开提供操作系统或随操作系统。

### <a name="source-media-for-inf-files"></a>INF 文件的源媒体

驱动程序的 INF 文件指定这些文件位于通过[ **SourceDisksNames** ](inf-sourcedisksnames-section.md)并[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)部分。 如果包含此类 INF **Include**并**需要**中的条目[ ***DDInstall*** ](inf-ddinstall-section.md)部分引用其他 INF 文件和部分中，这些文件和部分可以指定其他可能的源位置。

如果具有 INF **SourceDisksNames**并**SourceDisksFiles**部分，但不**Include**条目， **SourceDisksNames**和**SourceDisksFiles**部分必须列出所有的源媒体和驱动程序包除外目录中的源文件和 INF 文件。

目录文件必须位于与 INF 文件相同的位置。 不会压缩目录文件。 如果安装介质包括多个磁盘，然后*必须在每个磁盘上包含的 INF 和目录文件的单独副本*。 这是因为 INF 和目录文件必须仍可以访问在整个安装。

### <a name="source-media-and-inf-files-that-contain-include-and-needs-entries"></a>源媒体，并包含的 INF 文件包含和需求的条目

如果具有 INF [ **SourceDisksNames** ](inf-sourcedisksnames-section.md)并[ **SourceDisksFiles** ](inf-sourcedisksfiles-section.md)部分和**Include**和**需要**条目，Windows 使用的主要的 INF 文件以及任何包含的 INF 文件来查找源媒体。 它是与包含的文件是尽可能精确指定源媒体和源文件位置时尤其重要。

请考虑包含在下图中所示的 INF 文件的层次结构：

![说明包含的 inf 文件的示例层次结构的关系图](images/inf-hier.png)

此图显示了一个 INF 文件 (*MyMfDevice.inf)* 多功能设备。 此 INF 文件包含系统提供*Mf.inf*文件。 当 Windows 搜索要从其中复制文件中引用的源媒体*MyMfDevice.inf*，它会寻找**SourceDisksFiles**主题中*MyMfDevice.inf*和任何中包含的 INF 文件要复制的文件引用。 Windows 搜索*MyMfDevice.inf* ，但它并不保证其搜索包含的 INF 文件的顺序。

修饰**SourceDisksFiles**部分优先于未修饰的部分中，即使*修饰 INF 部分*中包含的文件。 例如，对于上图中所示的 INF 文件如果*Mf.inf*包含**\[SourceDisksFiles.x86\]** 部分和*MyMfDevice*.*inf*包含仅未修饰**\[SourceDisksFiles\]** 部分中，Windows 使用中的修饰的节*Mf.inf*x86 安装时的第一个计算机。 因此，包括其他 INF 文件 INF 应包含使用平台扩展的部分名称。

通常情况下，供应商提供 INF 应指定在文件的位置及其[驱动程序包](driver-packages.md)，应该不会导致 Windows 搜索包含的文件位置的 INF 文件。 换而言之，供应商 INF 文件复制应指定这两个**SourceDisksNames**和一个**SourceDisksFiles**部分中，应使用平台扩展和这些部分修饰这些部分应包含的 INF 直接复制的所有文件的信息。

供应商文件名称应该是一样的特定于供应商，以免潜在文件名冲突问题。

请注意，**包括**条目仅可用于指定系统提供的 INF 文件。

通过使用另一个 INF 文件中使用的区的 INF 文件**Include**并**需要**条目可能需要使用随附的部分来保持一致性。 例如，如果一个 INF 文件引用的安装部分 (*DDInstall*) 的另一个 INF 文件以安装该驱动程序，它必须引用[ **INF *DDInstall*。服务部分**](inf-ddinstall-services-section.md)安装随附的服务。 此类的 INF 文件可能具有以下各节：

```cpp
[DDInstall]
Include = AnotherINFFile.inf
Needs = AnotherINFFileDDInstall

[DDInstall.Services]
Include = AnotherINFFile.inf
Needs = AnotherINFFileDDInstall.Services
```

此外请注意每个部分，指定**需要**指令还必须指定**Include**指令，即使相同的 INF 文件中指定**Include**指令其他位置中 INF。

 

 





