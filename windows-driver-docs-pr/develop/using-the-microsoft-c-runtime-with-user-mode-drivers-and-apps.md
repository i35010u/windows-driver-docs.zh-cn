---
title: 使用含用户模式驱动程序和桌面应用的 Microsoft C 运行时
description: 本主题提供有关分发 Windows 8 和 Windows 8.1 应用程序和驱动程序的 C 运行时库的信息。
ms.date: 01/08/2021
ms.localizationpriority: medium
ms.openlocfilehash: c2aa3da09708b4dadc72e91bb703178bfa733c83
ms.sourcegitcommit: 04ae4617d30c65455f95065cc8a72f2ef650f35b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/21/2021
ms.locfileid: "98658220"
---
# <a name="using-the-microsoft-c-runtime-with-user-mode-drivers-and-desktop-apps"></a>使用含用户模式驱动程序和桌面应用的 Microsoft C 运行时

> [!NOTE]
> 本主题只适用于 Windows 桌面驱动程序，而不适用于 Windows 驱动程序。 若要了解此区别，请参阅 [Windows 驱动程序入门](getting-started-with-windows-drivers.md)。

如果要构建适用于 Windows 10 的应用程序或驱动程序，则只需要阅读本部分。 如果使用的 Visual Studio 版本早于 Visual Studio 2015，请跳过此部分，并从阅读[重新分发 C 运行时（适用于 Visual Studio 2015 之前的版本）](#redistributing-the-c-runtime-applies-to-before-visual-studio-2015)开始学习。

如果一开始使用的是 Visual Studio 2015，通用 C 运行时 (UCRT)包含了 C 运行时。 一个完整程序所需的其他部分（C/C++ 语言功能、C++ 库）由 VC++ 可再分发程序包中的 Visual Studio 提供。 为避免运行时再分发要求，这些部分是通过静态方式链接的。

> [!WARNING]
> 在 Visual Studio 中构建用户模式驱动程序项目时，如果将 **PlatformToolset** 设置为 `WindowsUserModeDriver10.0`，工具集会忽略项目中指定的任何运行时库，并针对 VC++ 运行时以静态方式链接，针对 UCRT 以动态方式链接。  使用此工具集时，无法重新配置此混合链接行为。

如果使用的不是 `WindowsUserModeDriver10.0` 工具集，则使用以下过程进行修改（例如，包含另一个 DLL）：

1. 设置为通常以静态方式链接：**属性 > C/C++ > 代码生成 > 运行时库 = 多线程 (/MT)**
2. 删除静态链接的 UCRT：**属性 > 链接器 > 输入 > 忽略特定默认库 += libucrt.lib**
3. 添加动态链接的 UCRT：**属性 > 链接器 > 输入 > 其他依赖项 += ucrt.lib**，**属性 > 链接器 > 输入 > 忽略特定默认库 += libucrt.lib**

## <a name="redistributing-the-c-runtime-applies-to-before-visual-studio-2015"></a>重新分发 C 运行时（适用于 Visual Studio 2015 之前的版本）

> [!NOTE]
> 从现在起下面的所有信息仅适用于 2015 之前的版本。 在 2015 版之前，有两个独立的 C 运行时版本：Visual C++ 运行时（VCRT，例如 `msvcr120.dll`）和旧版 WINDOWS CRT (`msvcrt.dll`)。  

Visual Studio 会将 VCRT 的最新版本安装到 `System32` 目录中。 如果文件不在此位置，可将其直接复制到 Visual C++ 项目的生成目录中。

如果用户模式驱动程序或桌面应用程序使用 VCRT，则必须分发相应的动态链接库。 使用 Visual C++ 可再发行程序包（`VCRedist_x86.exe`、`VCRedist_x64.exe`、`VCRedist_arm.exe`）。 将可再发行程序包链接到其他二进制文件，可再发行程序包将接收自动更新。

如果要实现隔离或避免对 VC ++ 可再分发程序包的依赖，可以改为静态链接到 CRT。 虽然非驱动程序项目通常能够将特定的 Visual C/C++ DLL 复制到应用程序本地文件夹（应用程序安装位置），以避免依赖于 VC ++ 可再分发程序包，但应用程序本地部署不适合驱动程序。

请使用可再发行程序包，而不要将单个 CRT 组件复制到 `System32`。 这可能导致不会自动为 CRT 提供服务，并且可能会覆盖它。

以下特别注意事项适用于打印机驱动程序：

-   这些驱动程序应会将所需的 CRT 文件包括到 INF 中，所以 CRT 文件将被作为驱动程序负载的一部分复制到驱动程序存储内。
-   V4 打印驱动程序无法使用辅助安装程序安装，所以 INF 必须将相关的 C/C++ 运行时库二进制文件复制到驱动程序存储内。 若要执行此操作，请在驱动程序包的 \[COPY\_FILES\] 部分中引用相应文件。
-   V3 打印驱动程序应不会使用辅助安装程序安装，因为它们不在“指向和打印”连接时运行。 这些驱动程序应当在驱动程序包的 **\[COPY\_FILES\]** 部分中引用相应文件。

以下示例说明了如何将 CRT 二进制文件包括在 INF 的 **\[COPY\_FILES\]** 部分中：

```inf
[COPY_FILES]
;CRT
Msvcr120.dll
; other files

* [SourceDisksFiles]
Msvcr120.dll = 2 
; other files

* [SourceDisksNames.amd64]
1 = %Location%,,,
2 = %Location%,,,"amd64"
```

对于 UMDF 驱动程序：

-   根据 CRT 静态链接驱动程序以在二进制文件中加入运行时。 在此情况下，你不需要重新分发 CRT。

## <a name="linking-your-code-with-the-c-runtime-libraries-applies-to-before-visual-studio-2015"></a>将代码与 C 运行时库链接（适用于 Visual Studio 2015 之前的版本）

若要确定必须为你的应用程序重新分发哪些 DLL，请收集你的应用程序所依赖的 DLL 的列表。 收集此列表的一种方法是运行依赖项查看器 (`depends.exe`)。

有关详细信息，请参阅[确定要重新分发的 DLL](/previous-versions/visualstudio/visual-studio-2013/8kche8ah(v=vs.120)) 和[选择部署方法](/previous-versions/visualstudio/visual-studio-2013/ms235316(v=vs.120))。

你无法重新分发 Visual Studio 中包括的所有文件；仅允许你重新分发 [Visual Studio 2013 Preview and Visual Studio 2013 SDK Preview 的可再发行代码](https://go.microsoft.com/fwlink/p/?linkid=320999)。 应用程序的调试版本和各个 Visual C++ 动态链接库不可以再分发。

以下库包含 C 运行时库功能：

|术语|说明|
|--- |--- |
|Msvcr120.dll|C 运行时|
|Msvcp120.dll|C++ 运行时|
|Msvcr120d.dll|C 运行时的调试版本 - 不允许再发行|
|Msvcp120d.dll|C++ 运行时的调试版本 - 不允许再发行|

