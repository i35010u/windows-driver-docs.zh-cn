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
ms.openlocfilehash: 0b957581c6c4adc7de84a7cb9228412e47493fa1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353452"
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

Microsoft Windows 硬件质量实验室 (WHQL) 测试程序使用用户模式显示驱动程序名称的列表来验证驱动程序二进制文件通过测试运行中保持不变。 其他应用程序可能还可以使用列表的用户模式显示驱动程序名称，通常通过[实现 WMI](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi) (WMI) 的应用程序确定的文件列表将将的一部分[驱动程序包](https://docs.microsoft.com/windows-hardware/drivers/install/components-of-a-driver-package).

 

 





