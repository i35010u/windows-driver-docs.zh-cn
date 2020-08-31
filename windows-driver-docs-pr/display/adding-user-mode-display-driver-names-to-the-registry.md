---
title: 将用户模式显示驱动程序名称添加到注册表
description: 将用户模式显示驱动程序名称添加到注册表
ms.assetid: 52f98ce5-4458-4058-9134-f57e4b56377f
keywords:
- INF 文件 WDK 显示，用户模式驱动程序名称
- 用户模式显示驱动程序 WDK Windows Vista，添加到注册表的名称
- 注册表 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92e2e87a252646deb10483585abb9c02b2cfb5e0
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063182"
---
# <a name="adding-user-mode-display-driver-names-to-the-registry"></a>将用户模式显示驱动程序名称添加到注册表


你必须在 INF 文件的 "外接程序" 部分中设置以下条目，以便在安装驱动程序时将用户模式显示驱动程序的名称添加到注册表中：

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, UserModeDriverName1, UserModeDriverName2, UserModeDriverNameWow1, UserModeDriverNameWow2
```

例如，对于 x86 计算机：

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, r200umd 
```

例如，对于 x64 计算机：

```inf
[Xxx_SoftwareDeviceSettings]
...
HKR,, InstalledDisplayDrivers,    %REG_MULTI_SZ%, r200umd, r200umdva, r200umd64, r200umd64va
```

Microsoft Windows 硬件质量实验室 (WHQL) 测试程序使用用户模式显示驱动程序名称列表来验证驱动程序二进制文件在测试运行中是否保持不变。 其他应用程序还可以使用用户模式显示驱动程序名称列表，通常通过 [实现 wmi](../kernel/implementing-wmi.md) (wmi) ，因为应用程序确定的文件列表是 [驱动程序包](../install/components-of-a-driver-package.md)的一部分。

 

