---
title: 支持在其他总线上的多功能设备
description: 支持在其他总线上的多功能设备
ms.assetid: 5fc78dc5-0553-4557-b188-a34810305061
keywords:
- 多功能设备 WDK，其他总线
- 即插即用 WDK 多功能设备
- ISA WDK 多功能设备
- USB WDK 多功能设备
- IEEE 1394 WDK 多功能设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dfaca1a4cd784bfed31773cc6ae01c2e311d0b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544861"
---
# <a name="supporting-multifunction-devices-on-other-buses"></a>支持在其他总线上的多功能设备





对于即插即用的 ISA、 USB、 或 IEEE 1394 总线上的多功能设备，父总线驱动程序如果设备符合标准的总线枚举各个函数。

对于此类设备，父总线驱动程序管理是驻留在单个的总线位置的多个设备的事实。 系统的其余部分，各个函数独立设备一样运行。

此类型的多功能设备的供应商必须执行以下操作：

-   确保设备符合设备将在其驻留的总线的规范。

-   为设备的每个函数提供即插即用功能驱动程序。

    由于系统提供总线驱动程序处理的多功能语义，功能的驱动程序可以是函数打包为单个设备时使用了相同驱动程序。

-   提供设备的每个函数的 INF 文件。

    INF 文件可以是函数打包为单个设备时，将使用的相同文件。 INF 文件不需要任何特殊的多功能语义。

 

 




