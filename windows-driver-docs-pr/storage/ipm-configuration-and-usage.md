---
title: IPM 配置和使用情况
description: IPM 配置和使用情况
ms.assetid: 95057785-e5b5-40ae-86e4-50bbf0014cef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3ffeb42fb0ff4439e984281f1d3cb90bb475f59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368755"
---
# <a name="ipm-configuration-and-usage"></a>IPM 配置和使用情况


默认情况下不启用 Storport 空闲电源管理 (IPM)。 它可以启用在注册表中的"EnableIdlePowerManagement"值设置为任何非零值的设备的硬件密钥的"StorPort"子项中。 这可以通过使用设备 INF 文件或手动使用注册表编辑器。

下面的示例文本显示了所要添加到你的设备的 INF 文件以启用 Storport 空闲电源管理功能。

```cpp
          [DDInstall.HW]
          ; Enables Storport IPM for this adapter
          HKR, "StorPort", "EnableIdlePowerManagement", 0x00010001, 0x01
```

这可以仅从 INF 文件 DDInstall.HW 部分 HKR 指向到硬件密钥而不是服务密钥的位置中。 有关如何更改 INF 文件的详细信息，请参阅[简介驱动程序的注册表项](https://go.microsoft.com/fwlink/p/?linkid=144533)。

电源选项控制面板小程序的以下屏幕截图显示用于配置系统电源策略和磁盘空闲超时值。 就可以从**启动** &gt; **控制面板** &gt; **电源选项**。

![演示如何 ipm 电源选项的屏幕截图](images/ipm-power-options.png)

命令行工具 (*Powercfg.exe*) 也可用。 类型**powercfg /？** 在命令提示符下使用情况信息。

 

 




