---
title: 启用 Direct3D 版本 10 DDI 的支持
description: 启用 Direct3D 版本 10 DDI 的支持
ms.assetid: ccbfecd2-8609-4e59-ac43-911f57af7980
ms.date: 10/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 899faf25e60aa78f38a008e0b6c284fbdae673bf
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065632"
---
# <a name="enabling-support-for-the-direct3d-version-10-ddi"></a>启用 Direct3D 版本 10 DDI 的支持


若要启用对用户模式显示驱动程序 DLL 的第10个 DDI 版本的支持，安装图形设备的显示驱动程序的 INF 文件必须列出 DLL 的名称，而不考虑 Direct3D 版本 10 DDI 是否与 [direct3d 版本 9](./direct3d-functions-implemented-by-user-mode.md#direct3d-version-9-functions) ddi 或单独的 dll 中存在。

[显示微型端口和用户模式显示驱动程序的安装要求](installing-display-miniport-and-user-mode-display-drivers.md)部分介绍了如何根据 Windows Vista 显示器驱动程序模型安装和使用用户模式显示驱动程序。 若要启用对 Direct3D 版本 10 DDI 的支持，必须在用户模式显示驱动程序名称列表中将包含版本 10 DDI 的 DLL 的名称指定为第二个项，即使版本 10 ddi 与版本 9 DDI 存在于同一 DLL 中也是如此。 下面的示例演示如何在 *Umd10*中包含第10版 ddi (（即版本 9 ddi) 中的单独 dll）时启用版本 10 ddi 支持：

```inf
[Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverName,    %REG_MULTI_SZ%, umd9.dll, umd10.dll
 HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, umd9, umd10 
```

下面的示例演示如何在 (*Umd*中包含第10版 ddi （与版本 9 ddi) 相同的 dll）时，如何启用版本 10 ddi 支持：

```inf
[Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverName,    %REG_MULTI_SZ%, umd.dll, umd.dll
 HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, umd, umd 
```

 

