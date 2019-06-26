---
title: 定义 WMI 实例名称
description: 定义 WMI 实例名称
ms.assetid: 0f91710a-7bd2-462a-b677-6dd32160a861
keywords:
- WMI WDK 内核，事件块
- 事件阻止 WDK WMI
- 数据将阻止 WDK WMI
- WMI WDK 内核，数据块
- 块 WDK WMI
- 动态实例名称 WDK WMI
- 静态实例名称 WDK WMI
- 实例的名称 WDK WMI
- WMI WDK 内核，实例名称
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33c0a37eae3a4be1bc428f14040cb44745cde398
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377099"
---
# <a name="defining-wmi-instance-names"></a>定义 WMI 实例名称





*实例*块的 WMI 包含由特定的物理设备或软件组件提供的数据。 就像一个块的 GUID 唯一地标识块，实例的名称唯一标识该实例的块。 WMI 客户端应用程序使用实例名称关联的数据块中使用的设备或提供数据的组件返回的信息。 WMI 使用实例名称来确定哪台设备的请求应发送到。 强烈建议定义实例名称时，驱动程序都将使用其 PDO。

驱动程序可以按两种方式之一定义块的实例的名称：

-   驱动程序通过一系列*静态实例名称*到 WMI 时它会注册块。

    注册了块后，驱动程序和 WMI 指定实例名称按其索引到此列表中。 可以基于静态实例名称*设备实例 ID*的驱动程序的 PDO，或驱动程序定义的基本名称; 或驱动程序可以定义一组实例名称字符串。 之前驱动程序显式更改它们的块重新注册之前，将始终保留静态实例名称。

-   驱动程序将生成*动态实例名称*创建实例时。

    该驱动程序指示，它会注册块时，它将生成的块的动态实例名称。 注册了块后，驱动程序和 WMI 传递动态实例名称作为字符串的缓冲区**Parameters.WMI.Buffer**。

仅当实例数或数据块的实例名称更改经常在运行时，驱动程序应生成动态实例名称。 例如，驱动程序可能使用进程 Id 或 TCP/IP 连接的 IP 地址作为实例名称。 此类的实例名称应为动态;如果它们是静态的驱动程序会产生相当大的开销，因为它必须调用[ **IoWMIRegistrationControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)发生变化。 每次更新的数量和实例的名称。

在大多数情况下，静态实例名称是优于动态实例名称，原因如下：

-   静态实例的名称提高驱动程序的性能，因为该驱动程序不需要在 WMI 请求的响应中返回实例名称字符串因为它必须为动态实例名称。

-   WMI 可以检测注册时的静态实例名称冲突，并自动修改实例名称，如有必要，以便所有实例名称都是唯一的给定块的无论多少驱动程序注册块。

    WMI 无法检测的动态实例名称的实例名称冲突，因此驱动程序负责生成使用的唯一名称[ **IoWMIAllocateInstanceIds**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiallocateinstanceids)。

-   驱动程序可以使用 WMI 库例程使用静态实例名称为块处理 Irp，只要名称基于驱动程序的 PDO 或驱动程序定义的基名称。

    驱动程序不能使用 WMI 库例程使用动态实例名称为数据块处理 Irp。

驱动程序指示应用程序块使用静态或动态实例名称，与静态实例的类型名称、 设置或清除 WMIREG\_标志\_*XXX*中[ **WMIREGGUID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmiregguidw)或[ **WMIGUIDREGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmiguidreginfo)结构它将传递给 WMI 注册块。 有关详细信息，请参阅[注册为 WMI 数据提供程序](registering-as-a-wmi-data-provider.md)。

 

 




