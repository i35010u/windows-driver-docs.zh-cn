---
title: 启用 Direct3D 版本 11 DDI 的支持
description: 启用 Direct3D 版本 11 DDI 的支持
ms.assetid: 997d6b06-110b-403d-bcf5-350a26ecffbd
keywords:
- Direct3D 11 版 WDK Windows 7 显示，从而启用 DDI 的支持
- Direct3D 11 版 WDK Windows Server 2008 R2 显示，从而启用 DDI 的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2718e45cffcccf29ba36316ae1a3b0471388417
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355576"
---
# <a name="enabling-support-for-the-direct3d-version-11-ddi"></a>启用 Direct3D 版本 11 DDI 的支持


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

若要启用支持的用户模式显示驱动程序 DLL 的版本 11 DDI、 INF 文件，安装了显示器驱动程序的图形设备必须列出无论 DLL 的名称的 Direct3D 版本 11 DDI 中存在相同 DLL 作为[Direct3D 版本 9 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/index)并[Direct3D 版本 10 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)或在单独的 DLL 中。

[显示微型端口和用户模式显示驱动程序的安装要求](installing-display-miniport-and-user-mode-display-drivers.md)部分介绍如何安装和使用 Windows Vista 显示器驱动程序模型根据用户模式显示驱动程序。 为启用还支持 Direct3D 版本 11 DDI，必须指定包含版本 11 的 DLL 的名称作为用户模式下的列表中的第三个项 DDI 显示驱动程序名称，即使 DDI 中存在的版本 11 版本 9 和 10 DDIs 作为同一个 DLL。

可以在多个位置使用同一个用户模式显示驱动程序 DLL 名称统一驱动程序实现。 实际上，设计的 Direct3D 版本 10 和 11 版 DDIs 强烈支持 Direct3D 版本 10 和 Direct3D 11 版驱动程序的共享的实施。

以下示例显示如何支持的版本 11 DDI 时启用版本 11 DDI 中包含*Umd11*.dll (即，单独从版本 9 和 10 DDIs DLL):

```inf
 [Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverName,    %REG_MULTI_SZ%, umd9.dll, umd10.dll,  umd11.dll
 HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, umd9, umd10, umd11 
```

以下示例显示如何支持的版本 11 DDI 时启用版本 11 DDI 中包含*Umd*.dll （即，共享的 Direct3D 版本 9、 10 和 11 的驱动程序实现）：

```inf
[Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverName,    %REG_MULTI_SZ%, umd.dll, umd.dll, umd.dll
 HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, umd, umd, umd 
```

 

 





