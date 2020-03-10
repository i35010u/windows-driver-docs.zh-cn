---
title: 使用通用 INF 文件
description: 如果要生成通用或移动驱动程序包，则必须使用通用 INF 文件。
ms.assetid: 2CBEB814-974D-4E8B-A44A-2CFAA8D4C94E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 517479adc9d31562812a27e2555839c2c55435e0
ms.sourcegitcommit: e1cfed28850a8208ea27e7a6a336de88c48e9948
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78402416"
---
# <a name="using-a-universal-inf-file"></a>使用通用 INF 文件

如果要生成通用或移动驱动程序包，则必须使用通用 INF 文件。 如果要生成桌面驱动程序包，则无需使用通用 INF 文件，但建议这样做，因为有性能好处。

通用 INF 文件使用可供 Windows 驱动程序使用的部分 [INF 语法](inf-file-sections-and-directives.md)。 通用 INF 文件可安装驱动程序并配置设备硬件，但不执行任何其他操作，例如运行辅助安装程序。

## <a name="why-is-a-universal-inf-file-required-on-non-desktop-editions-of-windows"></a>为什么 Windows 的非桌面版本上需要通用 INF 文件？

某些版本的 Windows（如 Windows 10 移动版）不支持适用于驱动程序安装的即插即用机制。 因此，驱动程序安装会在目标系统的脱机映像上进行。 Microsoft Visual Studio 在为此类目标系统生成驱动程序时，会生成一个基于 XML 的配置文件，其中包含要应用的所有注册表设置。 因此，此类系统的 INF 文件只能执行不依赖于系统运行时行为的添加操作。 使用此类受限语法的 INF 文件称为通用 INF 文件。

通用 INF 文件可以预测性地进行安装，每次的结果都相同。 安装结果不取决于系统的运行时行为。 例如，辅助安装程序引用在通用 INF 文件中无效，因为不能在脱机系统上执行其他 DLL 中的代码。

因此，可以提前配置包含通用 INF 文件的驱动程序包并将其添加到脱机系统。

可以使用 [InfVerif](../devtest/infverif.md) 工具来测试驱动程序的 INF 文件是否通用。

## <a name="which-inf-sections-are-invalid-in-a-universal-inf-file"></a>在通用 INF 文件中，哪些 INF 节无效？

可以使用通用 INF 文件中的任何 INF 节，以下节除外：

-   [**INF ClassInstall32 节**](inf-classinstall32-section.md)
-   [**INF DDInstall.CoInstallers 节**](inf-ddinstall-coinstallers-section.md)
-   [**INF DDInstall.FactDef 节**](inf-ddinstall-factdef-section.md)
-   [**INF DDInstall.LogConfigOverride 节**](inf-ddinstall-logconfigoverride-section.md)

只要 **TargetOSVersion** 修饰不包含 **ProductType** 标志或 **SuiteMask** 标志，[**INF Manufacturer 节**](inf-manufacturer-section.md)就有效。

## <a name="which-inf-directives-are-invalid-in-a-universal-inf-file"></a>在通用 INF 文件中，哪些 INF 指令无效？


可以使用通用 INF 文件中的任何 INF 指令，以下指令除外：

-   [**INF BitReg 指令**](inf-bitreg-directive.md)
-   [**INF DelFiles 指令**](inf-delfiles-directive.md)
-   [**INF DelProperty 指令**](inf-delproperty-directive.md)
-   [**INF DelReg 指令**](inf-delreg-directive.md)
-   [**INF DelService 指令**](inf-delservice-directive.md)
-   [**INF Ini2Reg 指令**](inf-ini2reg-directive.md)
-   [**INF LogConfig 指令**](inf-logconfig-directive.md)
-   [**INF ProfileItems 指令**](inf-profileitems-directive.md)
-   [**INF RegisterDlls 指令**](inf-registerdlls-directive.md)
-   [**INF RenFiles 指令**](inf-renfiles-directive.md)
-   [**INF UnregisterDlls 指令**](inf-unregisterdlls-directive.md)
-   [**INF UpdateIniFields 指令**](inf-updateinifields-directive.md)
-   [**INF UpdateInis 指令**](inf-updateinis-directive.md)

以下指令有效，但有一些注意事项：

-   如果指定的 *add-registry-section* 中的条目的 *reg-root* 值为 **HKR**，或处于以下情况，则 [**INF AddReg 指令**](inf-addreg-directive.md)有效：
    -   若要注册[组件对象模型](https://docs.microsoft.com/windows/desktop/com) (COM) 对象，可以在以下项下编写一个项：
        -   HKCR
        -   HKLM\SOFTWARE\Classes
    -   若要创建[硬件媒体基础转换](https://docs.microsoft.com/windows/desktop/medfound/media-foundation-transforms) (MFT)，可以在以下项下编写一个项：
        -   HKLM\SOFTWARE\Microsoft\Windows Media Foundation
        -   HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows Media Foundation
        -   HKLM\SOFTWARE\WOW3232Node\Microsoft\Windows Media Foundation

-   仅当[目标目录](inf-destinationdirs-section.md)为以下项之一时，[**INF CopyFiles 指令**](inf-copyfiles-directive.md)才有效：

    -   11（对应于 %WINDIR%\\System32）
    -   12（对应于 %WINDIR%\\System32\\Drivers）
    -   13（对应于用于存储驱动程序的 %WINDIR%\\System32\\DriverStore\\FileRepository 下的目录）  
            **注意：** CopyFiles 不能用于重命名特定的文件（**DestinationDirs** 包括与该文件相对应的 *dirid* 13）。 此外，*dirid* 13 仅在适用于数量有限的部分设备安装方案的 Windows 10 产品上有效。  如需更多详细信息，请参阅特定设备类的指南和示例。
    -   10,SysWOW64（对应于 %WINDIR%\\SysWOW64）
    -   10,*特定于供应商的子目录名称*  
            **注意：** 在 Windows 10 版本 1709 中，可以在使用 [InfVerif](../devtest/infverif.md) 工具来度量的通用 INF 中将 *dirid* 10 与特定于供应商的子目录名称配合使用。  在更高版本中，该值可能不受支持。  建议改用 *dirid* 13。

## <a name="see-also"></a>另请参阅

* [通用 Windows 驱动程序入门](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)
* [InfVerif](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif)
