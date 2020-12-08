---
title: INF 文件的源媒体
description: INF 文件的源媒体
keywords:
- INF 文件 WDK 设备安装，源媒体
- media WDK INF 文件
- 源媒体 WDK INF 文件
- 多功能设备 WDK INF 文件
- 修饰 INF WDK
- INF 文件 WDK 设备安装，单独装运
- 装运 INF 文件 WDK
- 单独交付 INF 文件 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ad197482be869a4c276346d01108da271022d57
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813093"
---
# <a name="source-media-for-inf-files"></a>INF 文件的源媒体





为设备文件指定源媒体时应使用的方法取决于 INF 文件是独立于操作系统提供，还是包含在操作系统中。

### <a name="source-media-for-inf-files"></a>INF 文件的源媒体

驱动程序的 INF 文件使用 [**SourceDisksNames**](inf-sourcedisksnames-section.md) 和 [**SourceDisksFiles**](inf-sourcedisksfiles-section.md) 部分指定文件的存放位置。 如果此类 inf 包含 [ * *_DDInstall_* _](inf-ddinstall-section.md)节中的 "**包括**" 和 "**需要**" 条目来引用其他 INF 文件和分区，则这些文件和分区可以指定其他可能的源位置。

如果 INF 有 _ *SourceDisksNames** 和 **SourceDisksFiles** 部分，并且没有 **包含** 条目，则 **SourceDisksNames** 和 **SourceDisksFiles** 部分必须列出驱动程序包中除目录和 INF 文件之外的所有源媒体和源文件。

目录文件必须与 INF 文件位于同一位置。 不得压缩目录文件。 如果安装介质包含多个磁盘，则 *每个磁盘上必须包含一个 INF 文件和目录文件的单独副本*。 这是因为在整个安装过程中必须可以继续访问 INF 和目录文件。

### <a name="source-media-and-inf-files-that-contain-include-and-needs-entries"></a>包含和需要条目的源媒体和 INF 文件

如果 INF 有 [**SourceDisksNames**](inf-sourcedisksnames-section.md) 和 [**SourceDisksFiles**](inf-sourcedisksfiles-section.md) 部分并 **包含** 和 **需要** 条目，则 Windows 将使用主 inf 文件以及所包含的任何 INF 文件来查找源媒体。 在指定源媒体和源文件位置时，尽可能精确地说明所包含的文件是非常重要的。

考虑下图中显示的包含的 INF 文件的层次结构：

![阐释包含的 inf 文件的示例层次结构的关系图](images/inf-hier.png)

此图显示了一个适用于多功能设备 (*MyMfDevice)* 的 inf 文件。 此 INF 文件包含系统提供的 *Mf .inf* 文件。 当 Windows 搜索要从中复制 *MyMfDevice* 中引用的文件的源媒体时，它将在 *MyMfDevice* 中以及引用要复制的文件的任何已包含 Inf 文件中查找 **SourceDisksFiles** 部分。 Windows 首先搜索 *MyMfDevice* ，但它不能保证搜索包含的 inf 文件的顺序。

修饰的 **SourceDisksFiles** 节优先于未修饰的部分，即使 *修饰的 INF 部分* 在包含的文件中也是如此。 例如，对于上图中显示的 INF 文件，如果 *Mf* 包含 **\[ \] SourceDisksFiles** 节和 *MyMfDevice*，则为。*inf* 仅包含未修饰的 **\[ SourceDisksFiles \]** 部分，Windows 在 x86 计算机上安装时，首先从 Mf 使用修饰部分 *。* 因此，包含其他 INF 文件的 INF 应包含使用平台扩展的部分名称。

通常情况下，供应商提供的 INF 应在其 [驱动程序包](driver-packages.md) 中指定文件的位置，而不应使 Windows 搜索包含的文件位置的 INF 文件。 换句话说，复制文件的供应商 INF 应同时指定 **SourceDisksNames** 和 **SourceDisksFiles** 部分，应使用平台扩展来修饰这些部分，这些部分应包含 INF 直接复制的所有文件的相关信息。

供应商文件名应尽可能与供应商相关，以避免潜在的文件名冲突。

请注意， **包含** 项仅可用于指定系统提供的 INF 文件。

通过使用 " **包括** " 和 " **需要** " 条目来使用另一个 inf 文件中的部分的 inf 文件，可能必须使用附带的部分来保持一致性。 例如，如果 INF 文件引用了安装部分 (*DDInstall*) 另一个 inf 文件来安装驱动程序，则它必须引用 [**inf *DDInstall*。服务部分**](inf-ddinstall-services-section.md) 来安装随附的服务。 此类 INF 文件可能包含以下部分：

```cpp
[DDInstall]
Include = AnotherINFFile.inf
Needs = AnotherINFFileDDInstall

[DDInstall.Services]
Include = AnotherINFFile.inf
Needs = AnotherINFFileDDInstall.Services
```

另请注意，指定 " **需要** " 指令的每个部分还必须指定 **包含** 指令，即使在 inf 中其他位置的 **Include** 指令中指定了同一 INF 文件也是如此。

 

 





