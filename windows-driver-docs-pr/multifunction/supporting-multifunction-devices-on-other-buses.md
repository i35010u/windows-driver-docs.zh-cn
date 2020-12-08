---
title: 支持其他总线上的多功能设备
description: 支持其他总线上的多功能设备
keywords:
- 多功能设备 WDK，其他总线
- PnP WDK 多功能设备
- ISA WDK 多功能设备
- USB WDK 多功能设备
- IEEE 1394 WDK 多功能设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1de4c8b51aaefc35d55362a3e2326e43a36325c4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840669"
---
# <a name="supporting-multifunction-devices-on-other-buses"></a>支持其他总线上的多功能设备





对于 PnP ISA、USB 或 IEEE 1394 总线上的多功能设备，如果设备符合总线标准，则父总线驱动程序会枚举各个函数。

对于这种设备，父总线驱动程序会管理有多个设备驻留在一个总线位置上的事实。 对于系统的其余部分，各个函数的运行方式类似于独立设备。

此类多功能设备的供应商必须执行以下操作：

-   确保设备符合设备将驻留的总线的规范。

-   为设备的每个功能提供 PnP 函数驱动程序。

    由于系统提供的总线驱动程序处理多功能语义，因此函数驱动程序可以是将函数打包为单个设备时使用的相同驱动程序。

-   为设备的每个功能提供一个 INF 文件。

    INF 文件可以是在将函数打包为单个设备时使用的相同文件。 INF 文件不需要任何特殊的多功能语义。

 

 




