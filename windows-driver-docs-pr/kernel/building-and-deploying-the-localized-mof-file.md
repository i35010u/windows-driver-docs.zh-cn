---
title: 生成和部署已本地化的 MOF 文件
description: 生成和部署已本地化的 MOF 文件
ms.assetid: 3a741dc6-a789-44e1-9d68-cdb41b7161ed
keywords:
- MOF 文件 WDK WMI
- 本地化 MOF 文件
- MUI 版本 WDK WMI
- 主 MOF 文件 WDK WMI
- 语言 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 215b9ae3d09a1b4d96297d4a51a0029d12d91716
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338612"
---
# <a name="building-and-deploying-the-localized-mof-file"></a>生成和部署已本地化的 MOF 文件





国际版本的 Windows XP 及更高版本的操作系统提供两种型号 — 单一语言 （本地化） 版本和多语言用户界面 (MUI) 版本。 Windows MUI 版本可以同时支持多种语言。

部署 Windows 的本地化版本的驱动程序应包含 MOF 资源，其中包含的所有类，以及本地化的语言修正合同和美国英语语言修正合同的非特定于语言的版本。

Windows MUI 版本，驱动程序图像本身应包含非特定语言和美国英语版本的 WMI 类。 对于每种附加语言支持，纯资源映像可以放在 %windir%\\system32\\驱动程序\\MUI\\*langid*目录，其中*langid*是 LCID 的区域设置。

（可选） 驱动程序图像本身可以包含受支持的每种语言。

如果其中一种机制不支持一种语言，则使用英语语言版本。

### <a name="building-distinct-mof-files-for-each-language"></a>为每种语言生成不同的 MOF 文件

驱动程序编写人员可以使用一个主 MOF 文本文件来包含基本类和所有其修正。

可以使用[MOF 编译器](compiling-a-driver-s-mof-file.md)生成包含非特定于语言的类，以及要包含已修正的类特定语言的文件的文件。

```cpp
mofcomp -amendment:namespace [ -MOF:mof] [ -MFL:mfl] masterfile
```

*命名空间*参数的形式 MS\_*XXX*，其中*XXX*是要生成的区域设置 LCID。 创建的 mof 文件包含非特定于语言的类，并创建 mfl 文件包含已修正的类。

在生成时您的驱动程序在基于 NT 的操作系统上，你可以通过使用复制命令来合并两个文件。 在 Windows 98 上 / 我，复制命令不会不正确追加 Unicode 文件，但可以使用以下命令。

```cpp
wmimofck localizedfile -ymof -zmfl
```

可以将任意数量的语言合并到一个文本文件。

本地化的文件可以然后将编译为二进制文件的未本地化的 MOF 文件与相同的方法：

```cpp
mofcomp -B:binaryfile localizedfile
```

有关单语言版本的 Windows，驱动程序将附加二进制 MOF 作为资源到驱动程序映像。 请参阅[编译的驱动程序的 MOF 文件](compiling-a-driver-s-mof-file.md)有关详细信息。

在 MUI 系统中，驱动程序图像本身必须生成针对美国英语。 对于每种附加语言安装每个二进制 MOF 文件本地化为适合的 %windir%中的单独的图像文件中的资源\\system32\\驱动程序\\MUI\\*langid*目录中，其中*langid*是区域设置 (例如，针对美国英语的 409) 的十六进制 LCID。 文件名称必须是*drivername.sys*或*drivername.sys*.mui，其中*drivername.sys*是二进制的驱动程序名称。

### <a name="building-one-mof-file-for-all-supported-languages"></a>有关所有支持的语言生成一个 MOF 文件

如果驱动程序映像将包含每个受支持的语言，则更简单的方法来构建支持每种语言的 MOF 文件。 通过使用**\#杂注**MOF 文本文件的驱动程序可以在指令还将合并的所有已修正类在同一二进制文件。 由于每个本地化存在于不同的命名空间中，它们可以安全地组合在单一的二进制文件中。

驱动程序编写人员在编写组合的 MOF 文本文件时，必须在与每个已修正的类声明之前**\#杂注**指令，如下所示

```cpp
#pragma namespace ("namespace")
```

其中`namespace`是正确的命名空间声明。 例如，美国英语的已修正的类声明前面必须加形式的声明：

```cpp
#pragma namespace ("\\\\.\\root\\wmi\\ms_409")
```

例如，您声明一个类和其修正，如下所示。

```cpp
#pragma namespace ("\\\\.\\root\\wmi)

[guid(xxxxxxxx-xxxx-xxxx-xxxxxxxxxxxx)]
class MyClass 
{
}

#pragma namespace(\\\\.\\root\\wmi\\ms_409)
[amendment, locale(0x407)]
class MyClass
{
}
```

使用此方法，生成二进制的 MOF 文件是相同的非本地化的方法。 请参阅[编译的驱动程序的 MOF 文件](compiling-a-driver-s-mof-file.md)有关详细信息。

 

 




