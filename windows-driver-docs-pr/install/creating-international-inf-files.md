---
title: 创建国际 INF 文件
description: 创建国际 INF 文件
keywords:
- INF 文件 WDK 设备安装，国际
- 国际 INF 文件 WDK
- 特定于区域设置的 INF 文件 WDK
- 特定于区域设置的驱动程序文件 WDK
- Unicode INF 文件 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9615b55d85d09c2672b1a5004479c8be48faa24
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827795"
---
# <a name="creating-international-inf-files"></a>创建国际 INF 文件





为国际化市场创建安装需要提供特定于区域设置的 INF 文件和特定于区域设置的驱动程序文件。

将在国际市场使用的 INF 文件应 **%** <em>strkey</em> **%** 为所有用户可查看文本使用 strkey 令牌。 这些字符串在 INF **字符串** 部分定义，通常在 inf 文件末尾。

### <a name="locale-specific-inf-files"></a>Locale-Specific INF 文件

你可以创建支持多个区域设置的单个 INF 文件，也可以按照以下准则为每个区域设置创建一个单独的 INF 文件：

- 若要创建单个国际 INF 文件，应包括一组特定于区域设置的 **字符串。**<em>LanguageID</em> 部分，如 [**INF 字符串**](inf-strings-section.md)的参考页中所述。 如果打算为所有国际市场提供单个安装介质，请使用此技术。

  对于 Windows 2000 及更高版本的 Windows 上的安装，建议使用这种方法来支持国际市场。

- 若要为每个区域设置单独创建一个 INF 文件，请从包含所有必需节和条目（ **字符串** 部分除外）的主 inf 文件开始。 然后，创建另一组文件，其中每个文件只包含支持的区域设置的 **字符串** 部分。 将主文件与每个字符串文件连接，以生成特定于区域设置的 INF 文件。

  对于 Windows 2000 及更高版本的 Windows 上的安装，仅当你打算为每个国际市场提供单独的安装介质时 *才* 使用此方法。 由于 Windows 无法确定要使用哪一个 INF 文件，因此不能在单个安装介质上为特定操作系统版本提供 INF 文件的多个版本。

### <a name="locale-specific-versions-of-driver-files"></a>驱动程序文件 Locale-Specific 版本

如果必须为 Windows 2000 和更高版本的 Windows 提供特定于区域设置的驱动程序文件版本，请使用每个文件的区域设置来标记每个文件的版本。 务必将不是特定于区域设置的文件标记为非特定语言。 为此，可以在资源文件中添加以下宏定义：

```cpp
#define VER_LANGNEUTRAL
```

此定义必须出现在包含 *common. ver* 的预处理器指令之前。

编译文件后，可以通过执行以下操作来验证每个文件是否被标记为非特定语言：

1.  右键单击 Windows 资源管理器中的文件。

2.  单击 **“属性”**。

3.  单击 " **版本** " 选项卡。

"**其他版本信息**" 窗格中的 **语言** 选择包含一个值，用于将文件标识为非特定语言或特定的区域设置。

将特定于区域设置的文件放在分发介质的单独的特定于区域设置的子目录中，如/*英语* 和/*德语*。 在 INF 文件中，执行以下操作：

-   在 [**INF SourceDisksFiles 部分**](inf-sourcedisksfiles-section.md)中，使用字符串密钥标记（如 **% LocaleSubDir%**）指定特定于区域设置的子目录。

-   为每种语言提供单独的 [**INF 字符串部分**](inf-strings-section.md) ，并在每个部分中定义相应的子目录名称字符串。

例如：

```cpp
[SourceDisksNames]
1=%DiskName%,,,%LocaleSubDir%

[SourceDisksFiles]
mysftwre.exe=1

[Strings]              ; No language ID implies English
DiskName="My Excellent Software"
LocaleSubDir="English"
[Strings.0407]         ; 0407 is the language ID for German
DiskName="Meine ausgezeichnete Software"
LocaleSubDir="German"
```

### <a name="creating-unicode-inf-files"></a>创建 Unicode INF 文件

如果 INF 文件包含的字符超出 ASCII 范围 (即在 0-127) 范围内，则 INF 文件应为 Unicode 格式。 创建 Unicode INF 文件的一种方法是使用记事本之类的应用程序以 Unicode 格式保存该文件。 如果 INF 未采用 Unicode 格式，则 Windows 将使用当前区域设置转换字符。 如果 INF 文件采用 Unicode 格式，则 Windows 将使用完整的 Unicode 字符集。

某些应用程序（如记事本）允许以小字节序或大字节序格式创建 Unicode 文件。 Windows 支持使用任意一种格式的 INF 文件。

 

 





