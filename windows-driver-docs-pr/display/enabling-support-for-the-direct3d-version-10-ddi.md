---
title: 启用 Direct3D 版本 10 DDI 的支持
description: 启用 Direct3D 版本 10 DDI 的支持
ms.assetid: ccbfecd2-8609-4e59-ac43-911f57af7980
ms.date: 10/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 24e2d6a58a784ea894eec8bfb506c36b74c90966
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379484"
---
# <a name="enabling-support-for-the-direct3d-version-10-ddi"></a>启用 Direct3D 版本 10 DDI 的支持


若要启用支持的 10 个 DDI、 INF 文件的用户模式显示驱动程序 DLL 的版本安装了显示器驱动程序的图形设备必须列出无论 DLL 的名称的 Direct3D 版本 10 DDI 中存在相同 DLL 作为[Direct3D 版本 9 DDI](https://docs.microsoft.com/windows-hardware/drivers/display/direct3d-functions-implemented-by-user-mode#direct3d-version-9-functions)或在单独的 DLL 中。

[显示微型端口和用户模式显示驱动程序的安装要求](installing-display-miniport-and-user-mode-display-drivers.md)部分介绍如何安装和使用 Windows Vista 显示器驱动程序模型根据用户模式显示驱动程序。 此外启用的 Direct3D 版本支持 10 个 DDI，则必须指定包含版本 10 的 DLL 的名称的用户模式显示驱动程序名称，即使列表中的第二个条目 DDI 10 DDI 存在于同一个 DLL 作为版本 9 DDI 的版本。 以下示例显示如何支持的版本 10 DDI 时启用版本 10 DDI 中包含*Umd10*.dll (即，单独的 DLL 版本为 9 版 DDI):

```inf
[Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverName,    %REG_MULTI_SZ%, umd9.dll, umd10.dll
 HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, umd9, umd10 
```

以下示例显示如何支持的版本 10 DDI 时启用版本 10 DDI 中包含*Umd*.dll (即，同一个 DLL 作为版本 9 DDI):

```inf
[Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverName,    %REG_MULTI_SZ%, umd.dll, umd.dll
 HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, umd, umd 
```

 

 





