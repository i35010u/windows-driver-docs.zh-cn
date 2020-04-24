---
title: 生成通用 Windows 驱动程序
description: 生成通用驱动程序指南
ms.date: 10/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 555cdead7ae3e80fc5835e9c724ad0552825da86
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "67370372"
---
# <a name="building-a-universal-windows-driver"></a>生成通用 Windows 驱动程序

可以将 Microsoft Visual Studio 2015 与 Windows 驱动程序工具包 (WDK) 10 结合使用来生成桌面版、移动版或通用版驱动程序。 可从 [Windows 硬件开发人员中心](https://go.microsoft.com/fwlink/p/?LinkId=524487)下载工具包和工具。

在许多情况下，可以将旧内核模式驱动程序重新编译为通用 Windows 驱动程序，前提是该驱动程序不使用任何用户模式组件。 旧 WDM 和 KMDF 驱动程序应该重新编译为针对 Windows 10 的通用 Windows 驱动程序，而无需转换。

相反，现有的用户模式驱动程序可能需要进行修改才能编译为通用 Windows 驱动程序。 具体来说，驱动程序包在 UWP 之外不能有任何依赖项。 例如，仅部分 Win32 API 属于 UWP。

## <a name="converting-an-existing-driver-project-to-a-universal-windows-driver-project"></a>将现有驱动程序项目转换为通用 Windows 驱动程序项目

1.  在 Visual Studio 2015 中，打开现有的驱动程序项目。
2.  在“解决方案资源管理器”窗格中，右键单击该解决方案，然后选择“配置管理器”  。 将目标操作系统设置为 Windows 10。
3.  右键单击该驱动程序项目，然后选择“属性”  。 在“配置属性”-&gt;“驱动程序”  下，确认将“目标平台”  设置为“通用”  。 其他选择包括“桌面”  （用于生成只在 Windows 10 桌面版上运行的驱动程序）和“移动”  （用于生成只在 Windows 10 移动版上运行的驱动程序）。
4.  生成驱动程序。 你可能会遇到链接器错误。
5.  浏览错误日志，逐个修复错误。 请参阅文档中的各个参考页面，以寻找可能的替换 API。 如果无法替换，则可能需要重新设计驱动程序。

## <a name="creating-a-new-universal-windows-driver-project-in-microsoft-visual-studio"></a>在 Microsoft Visual Studio 中创建新的通用 Windows 驱动程序项目

1.  使用模板创建新驱动程序（“文件”&gt;“新建项目”-&gt;“模板”-&gt;“Visual C++”-&gt;“Windows 驱动程序”-&gt;“WDF”  ），然后选择“用户模式驱动程序(UMDF V2)”  或“内核模式驱动程序(KMDF)”  。
2.  创建项目后，在“解决方案资源管理器”窗格中，右键单击该解决方案，然后选择“配置管理器”  。 将“活动解决方案配置”  设置为所需的目标 Windows 版本，并将“活动解决方案平台”  设置为“Win32”  或“x64”  。 如果 **ARM** 未列出，请选择“&lt;新建…&gt;”  为 ARM 生成。

    如果选择 Windows 10，驱动程序模型将默认为“通用”  。

    若要手动更改驱动程序模型，请右键单击驱动程序项目，然后选择“属性”。 在“配置属性”-&gt;“驱动程序设置”-&gt;“常规”  下，找到“目标平台”  条目。 选择“通用”  、“桌面”  或“移动”  。 Microsoft Visual Studio 使用此设置确定要链接的库。

    **注意**  无法为 Windows 10 之前的 Windows 版本生成通用 Windows 驱动程序。
3.  可能需要修改 .inf 文件以指定提供程序，指定为 %*ManufacturerName*% 令牌，该令牌稍后将在 INF 文件的 [**Strings**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section) 节中展开。 例如：

    ```cpp
    Provider="Contoso"
    ```

4.  现在可以生成解决方案。 Visual Studio 链接所需库并生成 .cat 文件、.inf 文件和驱动程序二进制文件。

## <a name="creating-a-new-universal-application-or-dll-project-in-microsoft-visual-studio"></a>在 Microsoft Visual Studio 中创建新的通用应用程序或 DLL 项目

1.  通过模板创建新的驱动程序（“文件”->“新建项目”->“模板”->“Visual C++”->“Windows 驱动程序”  ）并选择“适用于驱动程序的空桌面应用程序(通用)”  或“适用于驱动程序的空 Dll (通用)”  。
2.  创建项目后，在“解决方案资源管理器”窗格中，右键单击该解决方案，然后选择“配置管理器”  。 将“活动解决方案配置”  设置为所需的目标 Windows 版本，并将“活动解决方案平台”  设置为“Win32”  或“x64”  。 如果 ARM 未列出，请选择“<新建…>”  为 ARM 生成。
如果选择 Windows 10，应用程序模型将默认为“通用”  。
若要手动更改目标平台，请右键单击驱动程序项目，然后选择“属性”。 在“配置属性”->“驱动程序设置”->“常规”  下，找到“目标平台”  条目。
3.  生成解决方案。

有关生成驱动程序时可以在在 Visual Studio 中使用的配置设置的信息，请参阅[使用 WDK 生成驱动程序](building-a-driver.md)。
