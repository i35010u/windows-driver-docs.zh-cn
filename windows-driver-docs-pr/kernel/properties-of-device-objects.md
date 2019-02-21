---
title: 设备对象的属性
description: 设备对象的属性
ms.assetid: 6cd31263-e725-4a62-bec9-f40feb0b66cc
keywords:
- 设备对象 WDK 内核属性
- 属性 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69d8078747a880457274da3b83c994770359567e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521074"
---
# <a name="properties-of-device-objects"></a>设备对象的属性





每个设备对象具有特定属性，用于描述设备和设备对象与系统交互的方式。 设备对象属性包括：

-   设备类型。 指定的硬件设备的类型。 有关设备类型的详细信息，请参阅[指定设备类型](specifying-device-types.md)。

-   设备特征。 指定提供有关设备的其他信息的标志。 有关详细信息，请参阅[指定设备特征](specifying-device-characteristics.md)。

-   独占访问权限。 指定的设备对象是否表示*独占设备*。 如果设备是独占的只有一个句柄可以一次打开设备对象。 （如果基础设备支持重叠的 I/O，多个线程在相同的过程可以发送单个句柄通过的请求。）有关详细信息，请参阅[指定对设备对象的独占访问](specifying-exclusive-access-to-device-objects.md)。

-   安全描述符。 设备对象具有控制访问的安全描述符到设备。 有关详细信息，请参阅[保护设备对象](securing-device-objects.md)。

对于每个属性，创建设备对象时，可以设置默认值。 有关创建设备对象的详细信息，请参阅[创建一个设备对象](creating-a-device-object.md)。

此外可以在注册表中设置的设备对象属性的值。 请参阅[在注册表中设置设备对象属性](setting-device-object-properties-in-the-registry.md)有关详细信息。

 

 




