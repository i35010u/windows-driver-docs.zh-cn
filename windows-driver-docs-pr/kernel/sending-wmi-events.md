---
title: 发送 WMI 事件
description: 发送 WMI 事件
ms.assetid: 0d5e62f1-b84e-42b7-be40-8665f0b58ba8
keywords:
- WMI WDK 内核，事件跟踪
- 事件 WDK WMI
- 跟踪 WDK WMI
- 发送 WMI 事件
- 事件块 WDK WMI
- 通知 WDK WMI
- 动态实例名称 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b39c034afc5f6193bc122ebc0ad0e48980b74b88
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838434"
---
# <a name="sending-wmi-events"></a>发送 WMI 事件





驱动程序可以使用 WMI 事件通知用户模式的事件应用程序，而无需应用程序轮询或发送 Irp。 驱动程序应使用 WMI 事件通知 WMI 客户端异常情况，而不是作为错误日志记录的替代方法。 驱动程序应支持在 Wmicore 中为其设备类型定义的任何标准事件块，并可以定义和注册其他自定义事件块以支持特定于设备的通知。

事件块只是派生自抽象基类**register-wmievent**的数据块。 事件块可以包含与数据块相同的任何数据，也可以为空，即事件块不需要包含任何驱动程序定义的数据项。 如果事件块包含数据，则**WNODE\_* XXX*** 加数据的总大小不应超过注册表定义的限制 1 kb。 通常，较小的事件会导致更好的系统性能和更及时的通知。 有关定义块的信息，请参阅[Wmi 数据和事件块的 MOF 语法](mof-syntax-for-wmi-data-and-event-blocks.md)和[设计 Wmi 数据和事件块](designing-wmi-data-and-event-blocks.md)。

驱动程序通过使用 WMIREG\_标志注册相应的事件块来支持事件，\_事件\_仅\_块的[**WMIREGGUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)结构中设置的 GUID。 有关注册块的信息，请参阅[注册为 WMI 数据提供程序](registering-as-a-wmi-data-provider.md)。

当 WMI 客户端用户请求通知事件时，WMI 将发送[**IRP\_MN\_启用**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)对驱动程序的\_事件请求，这会提醒驱动程序开始监视事件的驱动程序确定的触发条件。 然后，当发生触发器条件时，驱动程序将事件发送到 WMI，后者将事件传递给已为该事件注册的所有数据使用者。

驱动程序通过以下方式之一将事件发送到 WMI：

- 调用内核模式 WMI 库例程[**WmiFireEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmifireevent)。 驱动程序可以调用**WmiFireEvent** ，以仅发送不使用动态实例名称的事件，以及将静态实例名称基于单个基名称字符串或 PDO 的设备实例 ID。 而且，该事件必须是单个实例，即，驱动程序无法调用**WmiFireEvent**来发送由单个项或多个实例构成的事件。 有关详细信息，请参阅[使用 WmiFireEvent 发送事件](sending-an-event-with-wmifireevent.md)。

- 使用指向包含事件数据的驱动程序分配的**WNODE\_* XXX*** 的结构的指针调用内核模式例程[**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent) 。 有关详细信息，请参阅[使用 IoWMIWriteEvent 发送事件](sending-an-event-with-iowmiwriteevent.md)。

 

 




