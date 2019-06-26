---
title: 串行连接的外围设备的连接 ID
description: 如果编写用于连接到串行端口由 SerCx2 管理的外围设备的驱动程序，驱动程序收到的硬件资源的列表将包含封装平台固件中的设备连接信息的连接 ID。
ms.assetid: 9A688552-DFAF-48A1-935D-70C3B13F30EC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e40a01b13fe414715421d6e938480075efe2359
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385232"
---
# <a name="connection-ids-for-serially-connected-peripheral-devices"></a>串行连接的外围设备的连接 ID

SerCx2 管理永久连接到外围设备的串行端口。 这些物理连接固定的因为它们可以在硬件平台的 ACPI 固件中所述。 如果编写用于连接到串行端口由 SerCx2 管理的外围设备的驱动程序，包括驱动程序收到的硬件资源的列表*连接 ID*封装设备连接信息从平台固件中。

在系统启动时，插即用 (PnP) 管理器枚举即插即用设备和非 PnP 设备。 对于非 PnP 外围设备具有固定的连接到串行端口，即插即用管理器将查询硬件平台的 ACPI 固件来获取一系列介绍如何访问设备的连接参数。 这些连接参数标识该设备连接到的端口的串行控制器，并包括其他信息，例如波特率速率和流控制设置，串行控制器所需的用于与设备进行通信。

PnP 管理器会分配连接的 ID 来表示此外围设备的连接参数。 PnP 管理器将此 ID 和连接参数一起调用的系统数据存储中存储*资源中心*。 （资源中心是 PnP 管理器将在其中存储有关串行连接的外围设备的配置信息的内部数据存储。）连接 ID 包装这些参数，以便外围设备驱动程序可以将其视为不透明。

外围设备驱动程序收到串行连接的外围设备的连接 ID 的驱动程序的一部分分配硬件资源。 当外围设备驱动程序调用系统函数，以打开到外围设备的连接时，驱动程序提供连接 ID，该系统函数用于从资源中心检索设备的连接参数。

连接 Id 用于打开逻辑连接到串行连接的外围设备的 UMDF 和 KMDF 驱动程序的代码示例，请参阅以下主题：

[连接到串行端口的外设的 UMDF 驱动程序](connecting-a-umdf-peripheral-device-driver-to-a-serial-port.md)

[连接到串行端口 KMDF 外围设备驱动程序](connecting-a-kmdf-peripheral-device-driver-to-a-serial-port.md)

打开到外围设备的串行端口上的连接的客户端具有独占访问权限端口，直到关闭的连接。 另一个客户端试图打开第二个连接到同一个端口无法正常工作。

打开串行端口之后, 客户端应假定端口处于未知或未定义状态。 客户端将负责配置端口，这样就可供使用。

若要配置的串行端口的操作，客户端发送 I/O 控制 (IOCTL) 请求到串行控制器。 通常情况下，客户端发送[ **IOCTL\_串行\_应用\_默认\_CONFIGURATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_apply_default_configuration)到控制器的请求，以将端口设置为其默认配置。 如有必要，客户端可以发送其他串行 Ioctl 重写一个或多个默认配置设置。 例如，Windows 定义串行 Ioctl 将波特率、 流控制参数、 线条控制设置和超时值更改为读取和写入请求。 有关支持的 SerCx2 串行 Ioctl 的列表，请参阅[串行 I/O 请求接口](serial-i-o-request-interface.md)。
