---
title: 发送 WMI 事件
description: 发送 WMI 事件
ms.assetid: 0d5e62f1-b84e-42b7-be40-8665f0b58ba8
keywords:
- WMI WDK 内核事件跟踪
- WDK WMI 事件
- 跟踪 WDK WMI
- 发送的 WMI 事件
- 事件阻止 WDK WMI
- 通知 WDK WMI
- 动态实例名称 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7684440ab645ea0979597bc319a9a544e60574a5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355132"
---
# <a name="sending-wmi-events"></a>发送 WMI 事件





驱动程序可以使用 WMI 事件通知的事件的用户模式应用程序而无需轮询和 / 或发送 Irp 的应用程序。 驱动程序应使用 WMI 事件通知的异常情况时，WMI 客户端不作为错误日志记录的替代方法。 驱动程序应支持 Wmicore.mof，在其设备类型定义的任何标准事件块和可能定义和注册其他自定义事件块，以支持特定于设备的通知。

事件块是只需一个数据块，派生的抽象基类**WMIEvent**。 事件块可以包含任何相同的数据的数据块，或可以为空，也即，事件块不需要包含任何驱动程序定义的数据的项。 如果事件块包含数据的总大小**WNODE\_* XXX*** 以及数据不应超过 1 千字节的注册表定义限制。 一般情况下，较小事件产生更好的系统性能和更及时的通知。 有关块定义的信息，请参阅[WMI 数据和事件块的 MOF 语法](mof-syntax-for-wmi-data-and-event-blocks.md)并[设计 WMI 数据和事件块](designing-wmi-data-and-event-blocks.md)。

驱动程序通过向 WMIREG 注册相应事件块指示事件的支持\_标志\_事件\_仅\_GUID 在块中设置[ **WMIREGGUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmiregguidw)结构。 有关注册块的信息，请参阅[注册为 WMI 数据提供程序](registering-as-a-wmi-data-provider.md)。

当 WMI 客户端用户请求事件的通知时，WMI 将发送[ **IRP\_MN\_启用\_事件**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)警报驱动程序以开始该驱动程序的请求监视事件的驱动程序确定触发器条件。 然后，触发器条件时，该驱动程序将事件发送到 WMI，它将其提供给已注册的事件的所有数据使用者。

驱动程序通过以下方式之一将事件发送到 WMI:

- 调用内核模式 WMI 库例程[ **WmiFireEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmifireevent)。 驱动程序可以调用**WmiFireEvent**发送唯一事件，不要使用动态实例名称和的基础单个基名称字符串或 PDO 的设备实例 ID 的静态实例名称。 此外，事件必须是单一实例-驱动程序不能调用，即**WmiFireEvent**发送事件的单个项或多个实例组成。 有关详细信息，请参阅[发送的事件 WmiFireEvent](sending-an-event-with-wmifireevent.md)。

- 调用内核模式例程[ **IoWMIWriteEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiwriteevent)用一个指针指向驱动程序分配并初始化**WNODE\_* XXX*** 结构，其中包含事件的数据。 有关详细信息，请参阅[发送的事件 IoWMIWriteEvent](sending-an-event-with-iowmiwriteevent.md)。

 

 




