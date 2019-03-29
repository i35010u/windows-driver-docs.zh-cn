---
title: 创建国际 INF 文件
description: 创建国际 INF 文件
ms.assetid: 7c07c4de-4a0f-4555-b153-15307c76a2a3
keywords:
- INF 文件 WDK 的设备安装，国际
- 国际 INF 文件 WDK
- 特定于区域设置的 INF 文件 WDK
- 区域设置特定于驱动程序文件 WDK
- Unicode INF 文件 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11b887103ebddb8d0962158f1fc40acdbfa9d4db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566091"
---
# <a name="creating-international-inf-files"></a>创建国际 INF 文件





创建适用于国际市场的安装要求提供特定于区域设置的 INF 文件以及可能的区域设置特定于驱动程序文件。

将国际市场中使用的 INF 文件应使用**%** <em>strkey</em> **%** 用户可查看的所有文本的令牌。 INF 中定义的字符串**字符串**部分中，这通常是 INF 文件末尾。

### <a name="locale-specific-inf-files"></a>特定于区域设置的 INF 文件

可以创建一个 INF 文件支持多个区域设置中，也可以创建一个单独的 INF 文件为每个区域设置，根据下列准则：

- 若要创建一个国际 INF 文件，应包括特定于区域设置的一组**字符串。**<em>LanguageID</em>节中的参考页所述[ **INF 字符串部分**](inf-strings-section.md)。 如果你想要提供所有的国际市场的单独的安装媒体，请使用此方法。

  对于 Windows 2000 和更高版本的 Windows 上的安装，这是支持国际市场的建议的方法。

- 若要创建每个区域设置单独的 INF 文件，开始使用主要的 INF 文件包含所有必要部分和条目，除**字符串**部分。 然后创建第二个集的文件，其中每个文件只包含**字符串**部分，了解支持的区域设置。 将连接与每个字符串文件来生成特定于区域设置的 INF 文件的主文件。

  对于 Windows 2000 和更高版本的 Windows 上的安装，使用此技术*仅*如果你想要提供每个国际市场的单独的安装媒体。 不能单独的安装介质上提供多个版本的用于特定操作系统版本的 INF 文件，因为 Windows 无法确定要使用的 INF 文件。

### <a name="locale-specific-versions-of-driver-files"></a>特定于区域设置版本的驱动程序文件

如果您必须为 Windows 2000 和更高版本的 Windows 提供特定于区域设置版本的驱动程序文件，将标记每个版本的每个文件与区域设置。 请确保标记不是作为非特定于语言的区域设置特定的文件。 可以通过将以下宏定义添加到的资源文件来执行此操作：

```cpp
#define VER_LANGNEUTRAL
```

此定义必须出现在之前包含预处理器指令*common.ver*。

在编译你的文件之后, 可以验证每个已通过执行以下标记为非特定语言的：

1.  右键单击 Windows 资源管理器中的文件。

2.  单击**属性**。

3.  单击**版本**选项卡。

**语言**中的所选内容**其他版本信息**窗格包含用于标识该文件作为非特定语言，或用于特定区域设置的值。

如将特定于区域设置的文件放入单独的、 特定于区域设置子目录分发介质的 /*英语*和 /*德语*。 在 INF 文件中，执行以下步骤：

-   内[ **INF SourceDisksFiles 部分**](inf-sourcedisksfiles-section.md)，如使用的字符串标记来指定特定于区域设置子目录 **%localesubdir%**。

-   提供单独[ **INF 字符串部分**](inf-strings-section.md)为每种语言，并在每个部分中定义的相应子目录名称字符串。

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

如果一个 INF 文件包含超出 ASCII 范围的字符 (即 0 到 127 这个范围之外)，INF 文件应采用 Unicode 格式。 若要创建 Unicode INF 文件的一种方法是使用记事本之类的应用程序以 Unicode 格式保存。 如果 INF 不是以 Unicode 格式，Windows 将使用当前区域设置字符转换。 如果 INF 文件是 Unicode 格式，Windows 将使用完整的 Unicode 字符集。

某些应用程序，如记事本，允许您以小 endian 或 big-endian 格式创建 Unicode 文件。 Windows 支持使用两种格式的 INF 文件。

 

 





