---
title: 设备对象的属性
description: 设备对象的属性
keywords:
- 设备对象 WDK 内核，属性
- 属性 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: efccbb01050f06c43b51e21c8da6c58d67791acc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805401"
---
# <a name="properties-of-device-objects"></a>设备对象的属性





每个设备对象都具有一些属性，这些属性描述设备以及设备对象如何与系统交互。 设备对象属性包括：

-   设备类型。 指定设备的硬件类型。 有关设备类型的详细信息，请参阅 [指定设备类型](specifying-device-types.md)。

-   设备特征。 指定提供有关设备的其他信息的标志。 有关详细信息，请参阅 [指定设备特征](specifying-device-characteristics.md)。

-   独占访问。 指定设备对象是否表示 *独占设备*。 如果设备是独占的，一次只能为设备对象打开一个句柄。  (如果基础设备支持重叠 i/o，则同一进程的多个线程可以通过一个句柄发送请求 ) 。有关详细信息，请参阅 [指定对设备对象的独占访问权限](specifying-exclusive-access-to-device-objects.md)。

-   安全描述符。 设备对象有一个控制对设备的访问的安全描述符。 有关详细信息，请参阅 [保护设备对象](controlling-device-access.md)。

对于每个属性，可以在创建设备对象时设置默认值。 有关创建设备对象的详细信息，请参阅 [创建设备对象](creating-a-device-object.md)。

还可以在注册表中设置设备对象属性的值。 有关详细信息，请参阅 [设置注册表中的设备对象属性](setting-device-object-properties-in-the-registry.md) 。

 

 




