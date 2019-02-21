---
title: 指定设备特征
description: 指定设备特征
ms.assetid: 8b73ed62-d611-4515-b9d0-8e0a37555a1a
keywords:
- 设备对象 WDK 内核，设备特征
- 设备特征 WDK 设备对象
- 标志 WDK 设备对象
- 设备堆栈 WDK 内核，设备特征
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1adc7d7d5416fd08aaacf3d1ab24c358335063f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533863"
---
# <a name="specifying-device-characteristics"></a>指定设备特征





每个设备对象可以具有一个或多个设备特征。 中的标志作为存储设备特征**特征**的设备对象的成员[**设备\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff543147)结构。

大多数驱动程序指定的文件仅\_设备\_SECURE\_打开特征。 这可确保到设备的命名空间相同的安全设置应用于任何打开的请求。 有关详细信息，请参阅[控制设备 Namespace 访问](controlling-device-namespace-access.md)。

该文件\_自动生成\_设备\_名称仅用于 PDOs。 该文件\_软盘\_软盘、 文件\_可移动\_媒体和文件\_编写\_一次\_媒体特征是特定于存储设备。 有关可能的设备特性标志的说明，请参阅的说明**特征**的成员[**设备\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff543147)。

某些设备特征，如文件\_自动生成\_设备\_名称，仅适用于单个设备对象。 在创建设备对象通过调用时，驱动程序可以指定单个设备对象的设备特征的设置[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)或[ **IoCreateDeviceSecure**](https://msdn.microsoft.com/library/windows/hardware/ff548407)。

以下特征适用于整个设备堆栈：

文件\_设备\_SECURE\_打开

文件\_软盘\_软盘

文件\_读取\_仅\_设备

FILE\_REMOVABLE\_MEDIA

文件\_编写\_一次\_媒体

驱动程序可以设置应用于整个设备堆栈的调用的设备特征**IoCreateDevice**或**IoCreateDeviceSecure**。 或者，可以在注册表中，任何一种设备或设备的安装程序类设置设备特性应用于整个设备堆栈。 (有关详细信息，请参阅[在注册表中设置设备对象属性](setting-device-object-properties-in-the-registry.md)。)

PnP 管理器确定设备特征的注册表设置，如下所示。

-   如果单个设备为指定值，即插即用管理器将使用该值;

-   否则，如果设备安装程序类指定一个值，即插即用管理器将使用该值;

-   否则，即插即用管理器使用零作为注册表设置的值。

如果在注册表中，设置适用于整个设备堆栈的设备特征，或者如果该属性设置为任何 FDO 或筛选器在堆栈中执行操作，然后 PnP 管理器将其设置为堆栈中的每个设备对象。 (如果设备处于*raw 模式*支持，并因此没有 FDO 则 PnP 管理器使用的是 PDO。)

 

 




