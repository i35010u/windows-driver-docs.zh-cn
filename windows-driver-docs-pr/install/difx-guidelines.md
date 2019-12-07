---
title: DIFx 指南
description: DIFx 指南
ms.assetid: de34f810-0e90-4626-b84d-160ac61541ad
ms.date: 05/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 265ef1ed226aeeb4ab0727a16676e8740b5f4e51
ms.sourcegitcommit: a97a623d64ddf573c760664be17778606e156cf5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2019
ms.locfileid: "74907117"
---
# <a name="difx-guidelines"></a>DIFx 指南

从 Windows 10 版本1607（Redstone 1）开始，驱动程序安装框架（DIFx）工具（`Difxapi.dll`、`Difxapp.dll`、`Difxappa.dll`和 `DPInst.exe`）已弃用，并且不再包含在 WDK 中。

相反，我们建议将[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)作为独立驱动程序包提供，不需要安装程序。  这是一个自包含包，它会添加其自己的设置或配置，而不是根据安装程序来修改系统状态。  需要单独的驱动程序包，才能可靠地支持所有驱动程序包方案。  发布独立驱动程序包的推荐方式是通过 Windows 更新。  执行此操作的第一步是向[Windows 硬件开发人员中心](https://partner.microsoft.com/dashboard)提交驱动程序包。

如果选择使用 DIFx，则必须使用较旧的 WDK 才能获得正确的工具。 以下注意事项适用：

* 如果驱动程序包仅指定 Windows 8.1 或更高版本的**TargetOSVersion**值，则不能使用 DIFxApp MSI 自定义操作，原因是 DIFxApp 依赖于[**GetVersionEx**](https://docs.microsoft.com/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getversionexa)，这是从 WINDOWS 8.1 开始更改的 API。  **TargetOSVersion**在[INF 制造商部分](inf-manufacturer-section.md)中指定。 DIFxApp 公开 MSI 自定义操作，例如 MsiProcessDrivers、MsiInstallDrivers 和 MsiUninstallDrivers。  如果驱动程序包指定 Windows 8.1 或更高版本的**TargetOSVersion**值，则不能在 MSI 中使用这些自定义操作。
* 从 Windows 8.1 开始，链接到 `Difxapi.dll` 的应用程序必须包含面向应用程序要在其上运行的操作系统版本的应用程序清单。  这是因为 DIFxAPI 依赖于[**GetVersionEx**](https://docs.microsoft.com/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getversionexa)，这是一个从 Windows 8.1 开始更改的 API。  有关 Windows 8.1 中的**GetVersionEx**更改的详细信息，请参阅[面向适用于 Windows 的应用程序](https://docs.microsoft.com/windows/desktop/SysInfo/targeting-your-application-at-windows-8-1)。
* 如果驱动程序包使用**TargetOSVersion**的***BuildNumber***部分（在 Windows 10 中引入，版本1607（版本14310及更高版本）），则不能将 DIFx 工具用于该驱动程序包。  DIFx 工具不支持 BuildNumber 目标。
* 使用 DIFx 版本2.1，该版本在 Windows 7 中通过 Windows 10 1511 版 WDK 提供。  尽管 DIFx 的早期版本中提供了2.1 版，但它与 Windows 7 和更高版本的 Windows 不兼容。

尽管不再进行更新，但你可以在[Difxapi](https://docs.microsoft.com/previous-versions/windows/hardware/difxapi/)中找到 DIFX 的 API 参考文档。

如果仍需要自定义安装程序来安装驱动程序包，请使用[PnPUtil](https://docs.microsoft.com/windows-hardware/drivers/devtest/pnputil)命令行工具或调用[驱动程序安装功能](functions-that-simplify-driver-installation.md)的自定义安装程序。

同样，如果需要自定义安装程序来卸载驱动程序包，请使用[PnPUtil](https://docs.microsoft.com/windows-hardware/drivers/devtest/pnputil)或调用[**DiUninstallDriver**](https://docs.microsoft.com/windows/win32/api/newdev/nf-newdev-diuninstalldriverw)或[**SetupUninstallOEMInf**](https://docs.microsoft.com/windows/win32/api/setupapi/nf-setupapi-setupuninstalloeminfw)的自定义安装程序。
