---
title: 注册表设置
description: 注册表设置
ms.assetid: a2536911-0467-4bd0-a63b-55341f0d7567
keywords:
- 游戏杆 WDK HID，注册表设置
- 虚拟游戏杆驱动程序 WDK HID，注册表设置
- VJoyD WDK HID，注册表设置
- 注册表 WDK 游戏杆
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31c6ce2ddbe8bec6737772a7011202fb3f8f1199
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345458"
---
# <a name="registry-settings"></a>注册表设置





操纵杆接口使用注册表来存储配置、 校准，以及用户首选项信息。 它还用于存储有关校准程序自定义的文本。 Windows 95/98/我游戏杆校准程序可以通过注册表来校准特定于游戏杆的过程中向用户提供的说明自定义。

值划分为五个组：

由 OEM 提供且 （如上所述） 的 INF 文件中安装的原始数据。

[用户值](user-values.md)，用于指定如何解释数据。

[当前设置](current-settings.md)专用于反映将当前配置的设备。

[保存设置](saved-settings.md)允许不同的配置未能召回。

[驱动程序设置](driver-settings.md)的设置的配置管理器设备设置。

用户的值、 当前设置，然后保存的设置是所有存储在注册表项下属于"当前"游戏杆驱动程序的路径。 每个游戏杆设备为其安装驱动程序都有一个键路径 REGSTR 下的\_路径\_JOYCONFIG 具有窗体 Msjstick.drv&lt;*xxxx*&gt;，其中*xxxx*是用来保留密钥名称唯一一个四位数字。 数与已安装的多媒体 （声音、 视频和游戏控制器） 驱动程序的数量相关。 在启动时 Msjstick.drv 将初始化为每个游戏控制器驱动程序的配置。 由于它只能处理一个配置一次，每个替换上一次，"当前"驱动程序是要初始化的最后一个。 这意味着用户可能会丢失所有当前设置，如果安装新的驱动程序，并且微型驱动程序不能在这些注册表值的路径将始终是相同的假设结构化。

 

 




