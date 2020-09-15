---
title: 使用通用 INF 文件
description: 如果要构建通用或移动驱动程序包，则必须使用通用 INF 文件。
ms.assetid: 2CBEB814-974D-4E8B-A44A-2CFAA8D4C94E
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: ac0268558f3cff0e097dbd28892c0615d3319e3e
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105718"
---
# <a name="using-a-universal-inf-file"></a>使用通用 INF 文件

如果要生成 [Windows 驱动](../develop/getting-started-with-windows-drivers.md) 程序包，则必须使用通用 INF 文件。 如果要生成 Windows 桌面驱动程序包，则无需使用通用 INF 文件，但建议这样做，因为性能有好处。

通用 INF 文件使用适用于 Windows 驱动程序的 [INF 语法](./general-syntax-rules-for-inf-files.md) 的子集。 通用 INF 文件安装驱动程序并配置设备硬件，但不执行任何其他操作，例如运行共同安装程序。

## <a name="why-is-a-universal-inf-file-required-on-non-desktop-editions-of-windows"></a>为什么 Windows 的非桌面版本上需要通用 INF 文件？

某些版本的 Windows （如 Windows 10）仅使用 Windows 10 Desktop 上提供的一部分驱动程序安装方法。 Windows 的非桌面版本的 INF 文件必须仅执行不依赖于系统运行时行为的加法运算。 带有此类受限语法的 INF 文件称为通用 INF 文件。

通用 INF 文件可预测安装，每次都具有相同的结果。 安装的结果不取决于系统的运行时行为。 例如，共同安装程序引用在通用 INF 文件中无效，因为不能在脱机系统上执行其他 DLL 中的代码。

因此，可以提前配置包含通用 INF 文件的驱动程序包，并将其添加到脱机系统。

你可以使用 [InfVerif](../devtest/infverif.md) 工具来测试你的驱动程序的 INF 文件是否是通用的。

## <a name="which-inf-sections-are-invalid-in-a-universal-inf-file"></a>通用 INF 文件中哪些 INF 部分无效？

你可以使用通用 INF 文件中的任何 INF 部分，如下所示：

-   [**INF ClassInstall32 节**](inf-classinstall32-section.md)
-   [**INF DDInstall.CoInstallers 节**](inf-ddinstall-coinstallers-section.md)
-   [**INF DDInstall.FactDef 节**](inf-ddinstall-factdef-section.md)
-   [**INF DDInstall.LogConfigOverride 节**](inf-ddinstall-logconfigoverride-section.md)

只要**TargetOSVersion**修饰不包含**ProductType**标志或**SuiteMask**标志， [**INF 制造商部分**](inf-manufacturer-section.md)就有效。

例如，仅当 [**INF DefaultInstall 部分**](inf-defaultinstall-section.md) 具有体系结构修饰时，它才有效 `[DefaultInstall.NTAMD64]` 。

## <a name="which-inf-directives-are-invalid-in-a-universal-inf-file"></a>通用 INF 文件中哪些 INF 指令无效？


您可以使用通用 INF 文件中的任何 INF 指令，如下所示：

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

-   如果指定的 "*添加注册表" 一节*中的条目的*注册表项根*值为**HKR**，或在以下情况下，则[**INF AddReg 指令**](inf-addreg-directive.md)有效：
    -   为了 (COM) 对象注册 [组件对象模型](/windows/desktop/com) ，可以使用以下项编写密钥：
        -   HKCR
        -   HKLM\SOFTWARE\Classes
    -   若要创建 [硬件媒体基础转换](/windows/desktop/medfound/media-foundation-transforms) (MFTs) ，可以使用以下内容编写密钥：
        -   HKLM\SOFTWARE\Microsoft\Windows 媒体基础
        -   HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows 媒体基础
        -   HKLM\SOFTWARE\WOW3232Node\Microsoft\Windows 媒体基础

-   仅当[目标目录](inf-destinationdirs-section.md)为下列项之一时， [**INF CopyFiles 指令**](inf-copyfiles-directive.md)才有效：

    -   11 (对应于% WINDIR% \\ System32) 
    -   12 (对应于% WINDIR% \\ System32 \\ 驱动程序) 
    -   13 (对应于% WINDIR% \\ System32 \\ DriverStore FileRepository 下的目录， \\ 其中) 存储了驱动程序。  
            **注意：**  CopyFiles 不能用于重命名 **DestinationDirs** 包括 *dirid* 13 的文件。 此外， *dirid* 13 仅在 Windows 10 产品上适用于有限的部分设备安装方案。  有关更多详细信息，请参阅特定设备类的指南和示例。
    -   10，SysWOW64 (对应于% WINDIR% \\ SysWOW64) 
    -   10个*特定于供应商的子目录名称*  
            **注意：** 在 Windows 10 1709 版中，将 *dirid* 10 与供应商特定子目录名称一起使用在通用 INF 中有效，使用 [InfVerif](../devtest/infverif.md) 工具来度量。  在更高版本中，可能不支持此值。  建议移动到 *dirid* 13。

## <a name="see-also"></a>另请参阅

* [Windows 驱动程序入门](../develop/getting-started-with-windows-drivers.md)
* [InfVerif](../devtest/infverif.md)