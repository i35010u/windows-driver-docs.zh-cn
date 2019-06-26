---
title: DIFx 指南
description: DIFx 指南
ms.assetid: de34f810-0e90-4626-b84d-160ac61541ad
ms.date: 05/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: d3d4f7406fc917970b83df21c74d3f2b94bf1737
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375313"
---
# <a name="difx-guidelines"></a>DIFx 指南

从 Windows 10 版本 1607 (Redstone 1) 开始，驱动程序安装框架 (DIFx) 工具不再包含在 WDK 中。  相反，我们建议作为一个独立包，不需要的安装程序，理想情况下通过 Windows Update 来提供您的驱动程序。  若要将您的驱动程序添加到 Windows 更新，第一步是提交到驱动程序包[Windows 硬件开发人员中心](https://partner.microsoft.com/dashboard)。

如果你选择仍要使用 DIFx，必须使用较旧的 WDK，它包含的工具，并且你应注意的几个需要注意的问题：

* 如果仅指定驱动程序包**TargetOSVersion**值的 Windows 8.1 或更高版本，不能使用 DIFxApp DIFxApp 的依赖关系由于[ **GetVersionEx**](https://docs.microsoft.com/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getversionexa)，API更改在 Windows 8.1 中启动的。  **TargetOSVersion**中指定[INF 制造商部分](inf-manufacturer-section.md)。 DIFxApp 公开 MSI MsiProcessDrivers、 MsiInstallDrivers 和 MsiUninstallDrivers 等自定义操作。  如果驱动程序包指定**TargetOSVersion**值的 Windows 8.1 或更高版本，不能在 MSI 中使用这些自定义操作。
* 在 Windows 8.1，链接到应用程序中启动`Difxapi.dll`必须包含应用程序清单以在其应用程序只应运行的 OS 版本为目标。  这是因为 DIFxAPI 的依赖项的[ **GetVersionEx**](https://docs.microsoft.com/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getversionexa)，更改在 Windows 8.1 中启动的 API。  有关对多个在更改**GetVersionEx**在 Windows 8.1，请参阅[面向 Windows 应用程序](https://docs.microsoft.com/windows/desktop/SysInfo/targeting-your-application-at-windows-8-1)。
* 如果驱动程序包使用***BuildNumber***的一部分**TargetOSVersion** (在 Windows 10，版本 1607年中引入 （生成 14310 及更高版本）)，不能与 DIFx 工具使用该驱动程序包。  DIFx 工具不了解 BuildNumber 目标。
* 使用 DIFx 版本 2.1，这是 Windows 7 WDK 通过 Windows 10 版本 1511 WDK 中可用。  虽然 2.1 DIFx 版本是早期版本的 WDK 中提供，但未正确地与 Windows 7 和更高版本的 Windows 兼容。

尽管它不能再更新时，可以找到在 DIFx 的 API 参考文档[Difxapi.h](https://docs.microsoft.com/previous-versions/windows/hardware/difxapi/)。

如果提供该驱动程序作为一个独立包，不需要安装程序不是一个选项，则命令行工具[PnPUtil](https://docs.microsoft.com/windows-hardware/drivers/devtest/pnputil)或使用自定义安装程序[驱动程序安装函数](setupapi-functions-that-simplify-driver-installation.md)可以用作安装文章的一部分。
