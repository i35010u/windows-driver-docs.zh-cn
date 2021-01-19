---
title: 使用含用户模式驱动程序和桌面应用的 Microsoft C 运行时
description: 本主题提供有关分发 Windows 8 和 Windows 8.1 应用程序和驱动程序的 C 运行时库的信息。
ms.date: 01/08/2021
ms.localizationpriority: medium
ms.openlocfilehash: e01a444174c06ae8402b1e813da6438342e2e2d4
ms.sourcegitcommit: 3af9ea49935f54b272da0b0d182e81416716f698
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2021
ms.locfileid: "98052562"
---
# <a name="using-the-microsoft-c-runtime-with-user-mode-drivers-and-desktop-apps"></a>使用含用户模式驱动程序和桌面应用的 Microsoft C 运行时

> [!NOTE]
> 本主题只适用于 Windows 桌面驱动程序，而不适用于 Windows 驱动程序。 若要了解此区别，请参阅 [Windows 驱动程序入门](getting-started-with-windows-drivers.md)。

本主题提供有关分发 Windows 8 和 Windows 8.1 应用程序和驱动程序的 C 运行时库的信息。 它为用户模式驱动程序和桌面应用程序编写人员提供了编译代码、并通过必要的 C 运行时库打包代码以重新分发的指南。

## <a name="span-idthe_c_runtime_libraries__crt__are_no_longer_shipped_as_a_windows_shared_componentspanspan-idthe_c_runtime_libraries__crt__are_no_longer_shipped_as_a_windows_shared_componentspanspan-idthe_c_runtime_libraries__crt__are_no_longer_shipped_as_a_windows_shared_componentspanthe-c-runtime-libraries-crt-are-no-longer-shipped-as-a-windows-shared-component"></a><span id="The_C_runtime_libraries__CRT__are_no_longer_shipped_as_a_Windows_shared_component"></span><span id="the_c_runtime_libraries__crt__are_no_longer_shipped_as_a_windows_shared_component"></span><span id="THE_C_RUNTIME_LIBRARIES__CRT__ARE_NO_LONGER_SHIPPED_AS_A_WINDOWS_SHARED_COMPONENT"></span>C 运行时库 (CRT) 不再以 Windows 共享组件的形式提供


过去，Microsoft 将 C 运行时库 (CRT) 作为 Window 共享系统组件分发。 在以前版本的 WDK 中，在生成驱动程序或传统 Windows 应用时，可以将代码与 CRT 的 Windows 系统版本链接。 Windows 8 发布后，C 运行时库不再被视为系统组件，你必须随你的用户模式驱动程序或桌面应用程序提供 CRT 的可再发行版本。 本主题讨论了这一变化的原因、C 运行时的新组件，以及生成桌面应用或驱动程序和重新分发 CRT 的策略。

## <a name="span-idwhy_did_microsoft_make_this_change_spanspan-idwhy_did_microsoft_make_this_change_spanspan-idwhy_did_microsoft_make_this_change_spanwhy-did-microsoft-make-this-change"></a><span id="Why_did_Microsoft_make_this_change_"></span><span id="why_did_microsoft_make_this_change_"></span><span id="WHY_DID_MICROSOFT_MAKE_THIS_CHANGE_"></span>Microsoft 为何进行这项更改？


C 运行时有两个独立的版本。 一个是内部 Windows 组件，另一个供应用程序和驱动程序开发人员使用，随 Visual Studio 提供。 这项更改的主要原因是为了保持一致性，同时支持向客户提供 CRT 服务。

在过去，应用程序有时链接到未安装正确 CRT DLL 版本的计算机上的 CRT 版本。 使用 CRT 的通用公共版本有助于解决此问题。

此外，维护 CRT 可能很复杂。 Visual C 团队计划随 Visual Studio 提供 CRT 的定期更新。 使用推荐的重新分发策略，你可以轻松地为你的应用程序选择这些更改。 而且，你无需担心 CRT 的 Windows 系统版本的更改会中断你的应用程序。

msvcrt.dll 现在是 Windows 所有并生成的系统组件。 它只供系统级别组件使用。 文件 msvcr110.dll (Visual Studio 2012) 或 msvcr120.dll (Microsoft Visual Studio 2013) 是 CRT 的新公开版本，供桌面应用程序和用户模式驱动程序开发人员使用。

Visual Studio 会将 VCRT 的最新版本安装到 `System32` 目录中。 如果文件不在此位置，可将其直接复制到 Visual C++ 项目的生成目录中。

如果用户模式驱动程序或桌面应用程序使用 VCRT，则必须分发相应的动态链接库。 使用 Visual C++ 可再发行程序包（`VCRedist_x86.exe`、`VCRedist_x64.exe`、`VCRedist_arm.exe`）。 将可再发行程序包链接到其他二进制文件，可再发行程序包将接收自动更新。

## <a name="span-idredistributing_the_c_runtime_spanspan-idredistributing_the_c_runtime_spanspan-idredistributing_the_c_runtime_spanredistributing-the-c-runtime"></a><span id="Redistributing_the_C_Runtime_"></span><span id="redistributing_the_c_runtime_"></span><span id="REDISTRIBUTING_THE_C_RUNTIME_"></span>重新分发 C 运行时

请使用可再发行程序包，而不要将单个 CRT 组件复制到 `System32`。 这可能导致不会自动为 CRT 提供服务，并且可能会覆盖它。

以下特别注意事项适用于打印机驱动程序：

Visual C/C++ 可再发行组件包 (VCRedist\_\*.exe) 作为应用程序提供。 如果你的安装包含可再发行组件包，最新版本将作为一个完整包在初始设置后安装在 System32 中，并使用 Microsoft 更新服务支持更新。 Visual C/C++ 可再发行组件包的所有组件均统一更新。

如果你是将单个 CRT 组件复制到 System32，而不是使用可再发行组件包，这些不会自动提供，并可能被意外覆盖。

如果驱动程序将 CRT 组件复制到 System32 且另一个程序在运行可再发行组件包，有可能出现问题：驱动程序安装的版本将被覆盖。 相反情况同样存在潜在问题。 如果某个程序运行可再发行组件包，并且驱动程序将早期版本的 CRT 组件复制到 System32，这可能会中断应用程序。 INF 安装过程只会对照 System32 中已经存在的库检查要安装的库的版本号，如果不同将会将其覆盖。

## <a name="span-idrecommended_strategiesspanspan-idrecommended_strategiesspanspan-idrecommended_strategiesspanrecommended-strategies"></a><span id="Recommended_Strategies"></span><span id="recommended_strategies"></span><span id="RECOMMENDED_STRATEGIES"></span>建议的策略


随你的驱动程序和应用程序重新分发 C/C++ 运行时时，请使用以下策略。

对于在 Program Files 下安装的应用程序：

-   使用 Visual C++ 可再发行组件包（VCRedist\_x86.exe、VCRedist\_x64.exe、VCRedist\_arm.exe），此包将 CRT 部署在 System32 下。 在此情况下，可再发行组件包可以自动更新。
-   或者，将 DLL 安装到应用程序的本地目录（直接复制到安装应用程序的目录），或静态链接到 CRT。 在此情况下，CRT 需要手动提供。

对于打印机驱动程序：

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

## <a name="span-idlinking_your_code_with_the_c_runtime_librariesspanspan-idlinking_your_code_with_the_c_runtime_librariesspanspan-idlinking_your_code_with_the_c_runtime_librariesspanlinking-your-code-with-the-c-runtime-libraries"></a><span id="Linking_your_code_with_the_C_Runtime_libraries"></span><span id="linking_your_code_with_the_c_runtime_libraries"></span><span id="LINKING_YOUR_CODE_WITH_THE_C_RUNTIME_LIBRARIES"></span>将代码与 C 运行时库相链接

若要确定必须为你的应用程序重新分发哪些 DLL，请收集你的应用程序所依赖的 DLL 的列表。 收集此列表的一种方法是运行依赖项查看器 (`depends.exe`)。

有关详细信息，请参阅[确定要重新分发的 DLL](/previous-versions/visualstudio/visual-studio-2013/8kche8ah(v=vs.120)) 和[选择部署方法](/previous-versions/visualstudio/visual-studio-2013/ms235316(v=vs.120))。


若要确定必须为你的应用程序重新分发哪些 DLL，应收集你的应用程序所依赖的 DLL 的列表。 收集此列表的一种方法是运行依赖项查看器 (depends.exe)。

如果你有依赖项列表，请将其与 [Visual Studio 2013 Preview 和 Visual Studio 2013 SDK Preview 的可再发行代码](https://go.microsoft.com/fwlink/p/?linkid=320999)中所述的文件列表对比。 有关详细信息，请参阅[确定要重新分发的 DLL](/previous-versions/visualstudio/visual-studio-2013/8kche8ah(v=vs.120)) 和[选择部署方法](/previous-versions/visualstudio/visual-studio-2013/ms235316(v=vs.120))。

你无法重新分发 Visual Studio 中包括的所有文件；仅允许你重新分发 [Visual Studio 2013 Preview and Visual Studio 2013 SDK Preview 的可再发行代码](https://go.microsoft.com/fwlink/p/?linkid=320999)。 应用程序的调试版本和各个 Visual C++ 动态链接库不可以再分发。

以下库包含 C 运行时库功能：

|术语|说明|
|--- |--- |
|Msvcr120.dll|C 运行时|
|Msvcp120.dll|C++ 运行时|
|Msvcr120d.dll|C 运行时的调试版本 - 不允许再发行|
|Msvcp120d.dll|C++ 运行时的调试版本 - 不允许再发行|

