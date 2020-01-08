---
title: 空闲电源管理配置和使用情况
description: 空闲电源管理配置和使用情况
ms.assetid: 95057785-e5b5-40ae-86e4-50bbf0014cef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15eaff4268d8cb30dfe8d827bbce7dfe75092785
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606519"
---
# <a name="idle-power-management-configuration-and-usage"></a>空闲电源管理配置和使用情况

默认情况下不启用 Storport 空闲电源管理（IPM）。 可以通过将设备硬件密钥的 "StorPort" 子项中的 "EnableIdlePowerManagement" 值设置为任何非零值，在注册表中启用此功能。 这可以通过使用设备 INF 文件或使用注册表编辑器手动完成。

以下示例文本显示了需要添加到设备的 INF 文件以启用 Storport IPM 功能的内容。

```cpp
          [DDInstall.HW]
          ; Enables Storport IPM for this adapter
          HKR, "StorPort", "EnableIdlePowerManagement", 0x00010001, 0x01
```

这只能在 INF 文件的 DDInstall 节中完成，其中 HKR 指向硬件密钥，而不是服务密钥。 有关如何更改 INF 文件的详细信息，请参阅[驱动程序的注册表项简介](https://go.microsoft.com/fwlink/p/?linkid=144533)。

下面屏幕截图中显示的 "电源选项" 控制面板小程序用于配置系统电源策略和磁盘空闲超时值。 可以从 "**开始**&gt;**控制面板"** &gt;**电源选项**访问它。

![阐释 ipm 电源选项的屏幕截图](images/ipm-power-options.png)

还可以使用命令行工具（*Powercfg*）。 键入**powercfg/？** 用于命令提示符下的使用情况信息。
