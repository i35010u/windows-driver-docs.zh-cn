---
title: 定义 WMI 实例名称
description: 定义 WMI 实例名称
ms.assetid: 0f91710a-7bd2-462a-b677-6dd32160a861
keywords:
- WMI WDK 内核，事件块
- 事件块 WDK WMI
- 数据块 WDK WMI
- WMI WDK 内核，数据块
- 阻止 WDK WMI
- 动态实例名称 WDK WMI
- 静态实例名称 WDK WMI
- 实例名称 WDK WMI
- WMI WDK 内核，实例名称
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1663e34ba1e37758d46282067ae92b167652cdc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828397"
---
# <a name="defining-wmi-instance-names"></a>定义 WMI 实例名称





WMI 块的*实例*包含特定物理设备或软件组件所提供的数据。 正如块 GUID 唯一标识块一样，实例的名称唯一地标识块的实例。 WMI 客户端应用程序使用实例名称将数据块中返回的信息与提供数据的设备或组件相关联。 WMI 使用实例名称来确定应将请求发送到哪个设备。 强烈建议在定义实例名称时，驱动程序使用其 PDO。

驱动程序可以通过以下两种方式之一定义块的实例名称：

-   当注册块时，驱动程序将*静态实例名称*的列表传递给 WMI。

    注册块后，驱动程序和 WMI 会通过其索引将实例名称指定到此列表中。 静态实例名称可以基于驱动程序的 PDO 的*设备实例 ID*或驱动程序定义的基名称;或驱动程序可以定义实例名称字符串的列表。 静态实例名称会一直保留，直到驱动程序通过重新注册块来显式更改它们。

-   创建实例时，驱动程序会生成*动态实例名称*。

    驱动程序指示它将在注册块时为块生成动态实例名称。 注册块后，驱动程序和 WMI 会将动态实例名称作为缓冲区中的字符串**传递。**

仅当数据块的实例数或实例名在运行时经常更改时，驱动程序才应生成动态实例名称。 例如，驱动程序可能将进程 Id 或 TCP/IP 连接的 IP 地址用作实例名称。 此类实例名称应为动态的;如果它们是静态的，则驱动程序会产生相当大的开销，因为在每次发生更改时，它都必须调用[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)来更新实例的数量和名称。

在大多数情况下，静态实例名称优于动态实例名称，原因如下：

-   静态实例名称改善了驱动程序的性能，因为驱动程序无需返回实例名称字符串来响应 WMI 请求，因为它必须用于动态实例名称。

-   WMI 可以在注册时检测静态实例名称冲突，并在必要时自动修改实例名称，使所有实例名称对于给定的块都是唯一的，无论有多少驱动程序注册块。

    WMI 无法检测动态实例名称的实例名称冲突，因此驱动程序负责使用[**IoWMIAllocateInstanceIds**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiallocateinstanceids)生成唯一名称。

-   只要名称基于驱动程序的 PDO 或驱动程序定义的基名称，驱动程序就可以使用 WMI 库例程处理使用静态实例名称的块的 Irp。

    驱动程序无法使用 WMI 库例程来处理使用动态实例名称的数据块的 Irp。

驱动程序通过在其传递到 WMI 的[**WMIREGGUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)或[**WMIGUIDREGINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmiguidreginfo) *结构中设置*或清除 WMIREG\_\_标志来指示块是使用静态实例名称还是静态实例名称的类型，注册块。 有关详细信息，请参阅[注册为 WMI 数据提供程序](registering-as-a-wmi-data-provider.md)。

 

 




