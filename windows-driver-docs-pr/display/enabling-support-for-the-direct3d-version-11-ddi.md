---
title: 启用 Direct3D 版本 11 DDI 的支持
description: 启用 Direct3D 版本 11 DDI 的支持
ms.assetid: 997d6b06-110b-403d-bcf5-350a26ecffbd
keywords:
- Direct3D 版本 11 WDK Windows 7 显示，启用 DDI 支持
- Direct3D 版本 11 WDK Windows Server 2008 R2 显示，启用 DDI 支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 701483d830241f68703f499286ed5b880a17083a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838954"
---
# <a name="enabling-support-for-the-direct3d-version-11-ddi"></a>启用 Direct3D 版本 11 DDI 的支持


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

若要启用对用户模式显示驱动程序 DLL 的第11个 DDI 版本的支持，则安装图形设备的显示驱动程序的 INF 文件必须列出 DLL 的名称，而不管 Direct3D 版本 11 DDI 是否存在于与[direct3d 版本 9 D 相同的 dll 中DI](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/index)和[Direct3D 版本 10 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)或在单独的 DLL 中。

[显示微型端口和用户模式显示驱动程序的安装要求](installing-display-miniport-and-user-mode-display-drivers.md)部分介绍了如何根据 Windows Vista 显示器驱动程序模型安装和使用用户模式显示驱动程序。 若要启用对 Direct3D 版本 11 DDI 的支持，必须在用户模式显示驱动程序名称列表中将包含版本 11 DDI 的 DLL 的名称指定为第三项，即使版本 11 DDI 与版本9和 10 DDIs 位于同一 DLL 中也是如此。

你可以在多个位置使用相同的用户模式显示驱动程序 DLL 名称来统一驱动程序实现。 事实上，Direct3D 版本10和版本 11 DDIs 的设计都支持 Direct3D 版本10和 Direct3D 版本11驱动程序的共享实现。

下面的示例演示如何在*Umd11*中包含第11版 ddi （即，版本9和 10 DDIs 的单独 dll）时启用第11版 ddi 的支持：

```inf
 [Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverName,    %REG_MULTI_SZ%, umd9.dll, umd10.dll,  umd11.dll
 HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, umd9, umd10, umd11 
```

下面的示例演示如果*Umd*中包含版本 11 ddi （即，Direct3D 版本9、10和11驱动程序的共享实现），如何启用版本 11 ddi 支持：

```inf
[Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverName,    %REG_MULTI_SZ%, umd.dll, umd.dll, umd.dll
 HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, umd, umd, umd 
```

 

 





