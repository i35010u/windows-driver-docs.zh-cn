---
title: 枚举的总线上的设备
description: 枚举的总线上的设备
ms.assetid: 5731db82-2bc8-4a8d-98f1-3977845f572c
keywords:
- 即插即用 WDK KMDF，总线枚举
- 插 WDK KMDF，总线枚举
- 总线枚举 WDK KMDF
- 枚举 WDK KMDF
- 子设备 WDK KMDF
- 列出子设备 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4952b68f29f3b0ce539255941764b63861182c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519308"
---
# <a name="enumerating-the-devices-on-a-bus"></a>枚举的总线上的设备


*总线枚举*是确定哪些子设备连接到父设备的操作。 父设备通常是总线适配器，但它也可以支持多个函数，如声卡的步骤，为其每个函数需要一组单独的驱动程序的设备。

内核模式驱动程序框架 (KMDF) 支持两种类型的总线枚举：

-   [静态枚举](static-enumeration.md)，这很容易实现，是理想选择，如果数字格式和类型的子设备不是特定于系统的不会更改之后硬件接通。

-   [动态枚举](dynamic-enumeration.md)，如果数量或类型的子设备更改从一台计算机到另一个应使用哪些。

总线驱动程序可以使用总线枚举的一个或两个的类型。

有关编写 KMDF 总线驱动程序的详细信息，请参阅[总线驱动程序开发基于 KMDF](https://msdn.microsoft.com/windows/hardware/gg463281)。

 

 





