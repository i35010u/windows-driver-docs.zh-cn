---
title: 使用通用 INF 文件
description: 如果要构建一个通用或移动设备的驱动程序包，必须使用通用 INF 文件。
ms.assetid: 2CBEB814-974D-4E8B-A44A-2CFAA8D4C94E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58f45248683bd487d421bb3503bfff6b5fabc881
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339440"
---
# <a name="using-a-universal-inf-file"></a>使用通用 INF 文件

如果要构建一个通用或移动设备的驱动程序包，必须使用通用 INF 文件。 如果要构建桌面驱动程序包，无需使用通用 INF 文件，但建议这样做是因为性能优势。

通用 INF 文件使用的一个子集[INF 语法](inf-file-sections-and-directives.md)提供的 Windows 驱动程序。 通用 INF 文件安装的驱动程序和配置设备的硬件，但不会执行任何其他操作，如运行辅助安装程序。

## <a name="why-is-a-universal-inf-file-required-on-non-desktop-editions-of-windows"></a>为什么是在非桌面版本的 Windows 所需的通用 INF 文件？

某些版本的 Windows，如 Windows 10 移动版的驱动程序安装不支持插机制。 因此，驱动程序安装都发生在目标系统的脱机映像。 当 Microsoft Visual Studio 会生成此类为目标系统驱动程序时，它生成包含所有要应用的注册表设置的基于 XML 的配置文件。 因此，此类系统的 INF 文件必须执行不依赖于系统的运行时行为仅累加性的操作。 具有此类受限制的语法的 INF 文件称为通用 INF 文件。

通用 INF 文件以可预测的方式，安装相同的结果每次使用。 安装结果不依赖于系统的运行时行为。 例如，辅助安装程序的引用不是有效通用 INF 文件中因为不能在脱机的系统上执行其他 DLL 中的代码。

因此，可以预先配置驱动程序包使用通用 INF 文件并将其添加到脱机系统。

可以使用[InfVerif](../devtest/infverif.md)工具要测试是否是通用驱动程序的 INF 文件。

## <a name="which-inf-sections-are-invalid-in-a-universal-inf-file"></a>INF 部分通用 INF 文件中是否无效？

在以下情况除外通用 INF 文件中，可以使用任何 INF 部分：

-   [**INF ClassInstall32 部分**](inf-classinstall32-section.md)
-   [**INF DDInstall.CoInstallers 部分**](inf-ddinstall-coinstallers-section.md)
-   [**INF DDInstall.FactDef 部分**](inf-ddinstall-factdef-section.md)
-   [**INF DDInstall.LogConfigOverride 部分**](inf-ddinstall-logconfigoverride-section.md)

[ **INF 制造商部分**](inf-manufacturer-section.md)有效，只要**TargetOSVersion**修饰不包含**ProductType**标志或**SuiteMask**标志。

## <a name="which-inf-directives-are-invalid-in-a-universal-inf-file"></a>通用 INF 文件中的 INF 指令是否无效？


在以下情况除外通用 INF 文件中，可以使用任何 INF 指令：

-   [**INF BitReg 指令**](inf-bitreg-directive.md)
-   [**INF DelFiles 指令**](inf-delfiles-directive.md)
-   [**INF DelProperty Directive**](inf-delproperty-directive.md)
-   [**INF DelReg 指令**](inf-delreg-directive.md)
-   [**INF DelService Directive**](inf-delservice-directive.md)
-   [**INF Ini2Reg 指令**](inf-ini2reg-directive.md)
-   [**INF LogConfig Directive**](inf-logconfig-directive.md)
-   [**INF ProfileItems 指令**](inf-profileitems-directive.md)
-   [**INF RegisterDlls 指令**](inf-registerdlls-directive.md)
-   [**INF RenFiles 指令**](inf-renfiles-directive.md)
-   [**INF UnregisterDlls 指令**](inf-unregisterdlls-directive.md)
-   [**INF UpdateIniFields Directive**](inf-updateinifields-directive.md)
-   [**INF UpdateInis Directive**](inf-updateinis-directive.md)

以下指令均有效存在一些注意事项：

-   [ **INF AddReg 指令**](inf-addreg-directive.md)有效如果中指定的条目*添加注册表部分*具有*reg 根*值**HKR**，或在以下情况下：
    -   用于注册[组件对象模型](https://msdn.microsoft.com/library/ee663262(v=vs.85).aspx)(COM) 对象可能在写入密钥：
        -   HKCR
        -   HKLM\SOFTWARE\Classes
    -   用于创建[硬件 Media Foundation 转换](https://msdn.microsoft.com/library/windows/desktop/ms703138.aspx)(Mft)，可能在写入密钥：
        -   HKLM\SOFTWARE\Microsoft\Windows Media Foundation
        -   HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows Media Foundation
        -   HKLM\SOFTWARE\WOW3232Node\Microsoft\Windows Media Foundation

-   [**INF CopyFiles 指令**](inf-copyfiles-directive.md)有效才[目标目录](inf-destinationdirs-section.md)是以下之一：

    -   11 (对应于 %WINDIR%\\System32)
    -   12 (对应于 %WINDIR%\\System32\\驱动程序)
    -   13 (对应于 %WINDIR%下的目录\\System32\\DriverStore\\资料库存储驱动程序)  
            **注意：** CopyFiles 不能为其重命名文件**DestinationDirs**包括*dirid* 13。 此外， *dirid* 13 是仅在 Windows 10 设备安装方案的受限子网的产品上有效。  请有关您的特定设备类的更多详细信息，参阅指南和示例。
    -   10，SysWOW64 (对应于 %WINDIR%\\SysWOW64)
    -   10，*供应商特定的子目录名称*  
            **注意：** 在 Windows 10 版本 1709，使用*dirid* 10 与供应商特定的子目录名称是测量使用通用 INF 中有效[InfVerif](../devtest/infverif.md)工具。  在更高版本中，可能不支持此值。  我们建议移到*dirid* 13。

## <a name="see-also"></a>请参阅

* [安装通用 Windows 驱动程序](https://msdn.microsoft.com/windows-drivers/develop/installing_a_universal_driver)
* [InfVerif](https://msdn.microsoft.com/library/windows/hardware/dn929319)
