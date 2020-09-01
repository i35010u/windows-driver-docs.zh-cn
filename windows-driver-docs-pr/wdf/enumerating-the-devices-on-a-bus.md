---
title: 枚举总线上的设备
description: 枚举总线上的设备
ms.assetid: 5731db82-2bc8-4a8d-98f1-3977845f572c
keywords:
- PnP WDK KMDF，总线枚举
- 即插即用 WDK KMDF，总线枚举
- 总线枚举 WDK KMDF
- 枚举 WDK KMDF
- 子设备 WDK KMDF
- 列出子设备 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 351915376119ae25dabbccd8d31fca0fa11296e8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185055"
---
# <a name="enumerating-the-devices-on-a-bus"></a>枚举总线上的设备


*总线枚举* 是确定哪些子设备连接到父设备的操作。 父设备通常是总线适配器，但也可以是支持多个功能（如声卡）的设备，每个功能需要一组单独的驱动程序。

内核模式驱动程序框架 (KMDF) 支持两种类型的总线枚举：

-   如果子设备的数量和类型并不特定于系统并且在插入硬件后不会更改，则可以轻松实现[静态枚举](static-enumeration.md)。

-   [动态枚举](dynamic-enumeration.md)，如果子设备的数量或类型从一台计算机更改为另一台计算机，则应使用该枚举。

总线驱动程序可以使用一种或两种类型的总线枚举。

有关编写 KMDF 总线驱动程序的详细信息，请参阅 [基于 KMDF 的总线驱动程序开发](/previous-versions/windows/hardware/design/dn613892(v=vs.85))。

 

