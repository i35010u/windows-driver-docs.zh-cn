---
title: 将用户模式显示驱动程序名称添加到注册表
description: 将用户模式显示驱动程序名称添加到注册表
ms.assetid: 52f98ce5-4458-4058-9134-f57e4b56377f
keywords:
- INF 文件 WDK 显示，用户模式驱动程序名称
- 用户模式显示驱动程序 WDK Windows Vista 中，添加到注册表的名称
- 注册表 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 823b56df8251bfcd2c3bc2843b6ecc0e8ccbc52b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341592"
---
# <a name="adding-user-mode-display-driver-names-to-the-registry"></a>将用户模式显示驱动程序名称添加到注册表


以便在驱动程序安装过程中向注册表添加的用户模式显示驱动程序的名称，必须在 INF 文件添加注册表部分设置以下条目：

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

Microsoft Windows 硬件质量实验室 (WHQL) 测试程序使用用户模式显示驱动程序名称的列表来验证驱动程序二进制文件通过测试运行中保持不变。 其他应用程序可能还可以使用列表的用户模式显示驱动程序名称，通常通过[实现 WMI](https://msdn.microsoft.com/library/windows/hardware/ff547139) (WMI) 的应用程序确定的文件列表将将的一部分[驱动程序包](https://msdn.microsoft.com/library/windows/hardware/ff539954).

 

 





