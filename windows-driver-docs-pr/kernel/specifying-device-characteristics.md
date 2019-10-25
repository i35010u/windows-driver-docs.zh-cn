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
ms.openlocfilehash: becb41a82fae8da5fb35dab78380fd0c183e8bcb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836294"
---
# <a name="specifying-device-characteristics"></a>指定设备特征





每个设备对象可以有一个或多个设备特征。 设备特征以标志的形式存储在设备对象的设备的**特征**成员中[ **\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构。

大多数驱动程序仅指定文件\_设备\_安全\_打开的特性。 这可确保将相同的安全设置应用到设备的命名空间中的任何打开的请求。 有关详细信息，请参阅[控制设备命名空间访问](controlling-device-namespace-access.md)。

\_设备\_名称自动生成的文件\_仅用于 PDOs。 文件\_\_软盘、文件\_可移动\_媒体和文件\_写入\_一次，\_媒体特性特定于存储设备。 有关可能的设备特征标志的说明，请参阅[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)的**特征**成员的描述。

某些设备特征（如文件\_自动生成\_设备\_名称）仅适用于单个设备对象。 驱动程序可以在通过调用[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)或[**IoCreateDeviceSecure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)创建设备对象时，为各个设备对象指定设备特征的设置。

以下特性适用于整个设备堆栈：

文件\_设备\_SECURE\_打开

文件\_软盘\_软盘

文件\_仅读取\_设备\_

文件\_可移动\_媒体

文件\_写入\_一次\_媒体

驱动程序可以通过调用**IoCreateDevice**或**IoCreateDeviceSecure**来设置适用于整个设备堆栈的设备特性。 或者，可以在注册表中为设备或设备的安装程序类设置适用于整个设备堆栈的设备特性。 （有关详细信息，请参阅[在注册表中设置设备对象属性](setting-device-object-properties-in-the-registry.md)。）

PnP 管理器按如下方式确定设备特征的注册表设置。

-   如果为单个设备指定了值，则 PnP 管理器将使用该值;

-   否则，如果为设备安装程序类指定了值，则 PnP 管理器将使用该值;

-   否则，PnP 管理器使用零值作为注册表设置。

如果在注册表中设置了应用于整个设备堆栈的设备特征，或在堆栈中为任何 FDO 或筛选器设置了该特征，则 PnP 管理器会为堆栈中的每个设备对象设置该特征。 （如果设备支持*raw 模式*，因此没有 FDO，则 PnP 管理器会改用 PDO。）

 

 




