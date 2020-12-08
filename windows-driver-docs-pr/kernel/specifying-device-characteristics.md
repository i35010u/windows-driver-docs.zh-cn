---
title: 指定设备特征
description: 指定设备特征
keywords:
- 设备对象 WDK 内核，设备特征
- 设备特征 WDK 设备对象
- 标志 WDK 设备对象
- 设备堆栈 WDK 内核，设备特征
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbdde740c9de8aef4096ca531a6cdd680cd5d085
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837955"
---
# <a name="specifying-device-characteristics"></a>指定设备特征





每个设备对象可以有一个或多个设备特征。 设备特征以标志的形式存储在设备对象的 [**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构的 **特征** 成员中。

大多数驱动程序仅指定文件 \_ 设备 \_ 安全 \_ 打开的特性。 这可确保将相同的安全设置应用到设备的命名空间中的任何打开的请求。 有关详细信息，请参阅 [控制设备命名空间访问](controlling-device-namespace-access.md)。

文件自动 \_ 生成 \_ 设备 \_ 名称仅用于 PDOs。 文件 \_ 软盘 \_ 、文件 \_ 可移动 \_ 介质和文件 \_ 写入 \_ \_ 介质特性特定于存储设备。 有关可能的设备特征标志的说明，请参阅 [**device \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)的 **特征** 成员的描述。

某些设备特征（如文件自动 \_ 生成 \_ 设备 \_ 名称）仅适用于单个设备对象。 驱动程序可以在通过调用 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) 或 [**IoCreateDeviceSecure**](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)创建设备对象时，为各个设备对象指定设备特征的设置。

以下特性适用于整个设备堆栈：

文件 \_ 设备 \_ 安全 \_ 打开

文件 \_ 软盘 \_

文件 \_ 只读 \_ \_ 设备

文件 \_ 可移动 \_ 介质

文件 \_ 写入 \_ 一次 \_ 介质

驱动程序可以通过调用 **IoCreateDevice** 或 **IoCreateDeviceSecure** 来设置适用于整个设备堆栈的设备特性。 或者，可以在注册表中为设备或设备的安装程序类设置适用于整个设备堆栈的设备特性。  (有关详细信息，请参阅 [在注册表中设置设备对象属性](setting-device-object-properties-in-the-registry.md)。 ) 

PnP 管理器按如下方式确定设备特征的注册表设置。

-   如果为单个设备指定了值，则 PnP 管理器将使用该值;

-   否则，如果为设备安装程序类指定了值，则 PnP 管理器将使用该值;

-   否则，PnP 管理器使用零值作为注册表设置。

如果在注册表中设置了应用于整个设备堆栈的设备特征，或在堆栈中为任何 FDO 或筛选器设置了该特征，则 PnP 管理器会为堆栈中的每个设备对象设置该特征。  (如果设备支持 *raw 模式* ，因此没有 FDO，则 PnP 管理器会改用 PDO。 ) 

 

