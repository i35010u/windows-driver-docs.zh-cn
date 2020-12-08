---
title: 生成和部署已本地化的 MOF 文件
description: 生成和部署已本地化的 MOF 文件
keywords:
- MOF 文件 WDK WMI
- 本地化 MOF 文件
- MUI 版本 WDK WMI
- 主 MOF 文件 WDK WMI
- 语言 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ee280c73024d7c646e56bfa324489fa3f7bcd00
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838785"
---
# <a name="building-and-deploying-the-localized-mof-file"></a>生成和部署已本地化的 MOF 文件





Windows XP 和更高版本操作系统的国际版本分为两种风格：单一语言 (本地化) 版本和多语言用户界面 (MUI) 版本。 MUI 版本的 Windows 可以同时支持多种语言。

在本地化版本的 Windows 上部署的驱动程序应包含一项 MOF 资源，其中包含所有类的非特定语言版本，以及本地化的语言修订和美国英语修正。

在 Windows 的 MUI 版本中，驱动程序映像本身应包含 WMI 类的非特定语言和美国英语版本。 对于支持的每种其他语言，只能在% windir% \\ system32 驱动程序 MUI langid 目录中放置一个纯资源映像 \\ \\ \\ *langid* ，其中 *LANGID* 是该区域设置的的 LCID。

驱动程序映像本身也可以包含支持的所有语言。

如果某个语言不支持这种机制，则使用英语版本。

### <a name="building-distinct-mof-files-for-each-language"></a>为每种语言构建不同的 MOF 文件

驱动程序编写者可以使用一个主 MOF 文本文件来包含基本类及其所有修正。

您可以使用 [MOF 编译器](compiling-a-driver-s-mof-file.md) 生成包含非特定语言类的文件，并使用一个文件来包含特定语言的修改后的类。

```cpp
mofcomp -amendment:namespace [ -MOF:mof] [ -MFL:mfl] masterfile
```

*命名空间* 参数的格式为 MS \_ *XXX*，其中 *XXX* 是要生成的区域设置的 LCID。 创建的 mof 文件包含非特定语言类，并且创建的 mfl 文件包含修改后的类。

在基于 NT 的操作系统上构建驱动程序时，可以使用复制命令合并这两个文件。 在 Windows 98/Me 上，复制命令无法正确地追加 Unicode 文件，但可以使用以下命令。

```cpp
wmimofck localizedfile -ymof -zmfl
```

可以将任意数量的语言组合到一个文本文件中。

然后，可以使用与未本地化的 MOF 文件相同的方法将本地化文件编译为二进制文件：

```cpp
mofcomp -B:binaryfile localizedfile
```

对于单语言版本的 Windows，驱动程序将二进制 MOF 作为资源附加到驱动程序映像。 有关详细信息，请参阅 [编译驱动程序的 MOF 文件](compiling-a-driver-s-mof-file.md) 。

在 MUI 系统上，必须为美国英语构建驱动程序映像本身。 对于每个其他语言，请在相应的% windir% system32 驱动程序 MUI langid 目录的单独映像文件中安装每个本地化的二进制 MOF 文件作为资源 \\ \\ \\ \\ *langid* ，其中 *langid* 是区域设置的十六进制 LCID (例如，409表示美国英语) 。 文件名必须是 *drivername.sys* 或 *drivername.sys* mui，其中 *drivername.sys* 是驱动程序二进制文件的名称。

### <a name="building-one-mof-file-for-all-supported-languages"></a>为所有支持的语言生成一个 MOF 文件

如果驱动程序映像将包含每种支持的语言，则可以通过一种更简单的方法来生成支持每种语言的 MOF 文件。 通过在 MOF 文本文件中使用 **\# 杂注** 指令，驱动程序还可以将所有修改后的类组合到一个二进制文件中。 由于每个本地化均存在于不同的命名空间中，因此可以安全地将它们合并到单个二进制文件中。

在写入合并的 MOF 文本文件时，驱动程序编写器必须在每个修改后的类声明之前包含 **\# 杂注** 指令，如下所示

```cpp
#pragma namespace ("namespace")
```

其中 `namespace` ，是声明的正确命名空间。 例如，对于美国英语，修改后的类声明必须采用以下形式的声明：

```cpp
#pragma namespace ("\\\\.\\root\\wmi\\ms_409")
```

例如，按如下所示声明类及其修正。

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

使用此方法，生成二进制 MOF 文件与非本地化方法相同。 有关详细信息，请参阅 [编译驱动程序的 MOF 文件](compiling-a-driver-s-mof-file.md) 。

 

 




