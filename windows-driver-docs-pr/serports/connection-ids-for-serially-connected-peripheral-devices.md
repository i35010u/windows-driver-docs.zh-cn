---
title: 串行连接的外围设备的连接 ID
description: 如果为连接到由 SerCx2 管理的串行端口的外围设备编写驱动程序，则该驱动程序接收的硬件资源列表包括一个连接 ID，该 ID 封装了平台固件中的设备连接信息。
ms.assetid: 9A688552-DFAF-48A1-935D-70C3B13F30EC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b27ba7f0a727e3d469db2129308c0a33062e9896
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187005"
---
# <a name="connection-ids-for-serially-connected-peripheral-devices"></a>串行连接的外围设备的连接 ID

SerCx2 管理要将外围设备永久连接到的串行端口。 由于这些物理连接是固定的，因此可以在硬件平台的 ACPI 固件中对其进行描述。 如果为连接到由 SerCx2 管理的串行端口的外围设备编写驱动程序，则该驱动程序接收的硬件资源列表包括一个 *连接 ID* ，该 ID 封装了平台固件中的设备连接信息。

系统启动时，即插即用 (PnP) manager 将同时枚举 PnP 设备和非 PnP 设备。 对于具有与串行端口的固定连接的非 PnP 外围设备，PnP 管理器会查询硬件平台的 ACPI 固件，以获取描述如何访问设备的一组连接参数。 这些连接参数标识设备连接到的端口的串行控制器，并包括串行控制器与设备通信所需的其他信息，如波特率和流控制设置。

PnP 管理器分配一个连接 ID 以表示此外围设备的连接参数。 PnP 管理器将此 ID 和连接参数一起存储在名为 *资源中心*的系统数据存储中。  (资源中心是一种内部数据存储，其中 PnP 管理器存储与串行连接的外围设备有关的配置信息。 ) 连接 ID 封装这些参数，以便外围设备驱动程序可以将它们视为不透明。

外围设备驱动程序接收串行连接外围设备的连接 ID 作为驱动程序分配的硬件资源的一部分。 当外设驱动程序调用系统函数以打开与外围设备的连接时，驱动程序会提供连接 ID，系统函数使用该 ID 从资源中心检索设备的连接参数。

有关使用连接 Id 打开连接到串行连接外围设备的逻辑连接的 UMDF 和 KMDF 驱动程序的代码示例，请参阅以下主题：

[将 UMDF 外设驱动程序连接到串行端口](connecting-a-umdf-peripheral-device-driver-to-a-serial-port.md)

[将 KMDF 外设驱动程序连接到串行端口](connecting-a-kmdf-peripheral-device-driver-to-a-serial-port.md)

在连接关闭之前，与串行端口上的外围设备的连接打开的客户端具有对端口的独占访问权限。 其他客户端尝试再次连接同一端口失败。

打开串行端口之后，客户端应假设端口处于未知或未定义状态。 客户端负责配置端口，使其可供使用。

若要配置串行端口以进行操作，客户端会将 (IOCTL) 请求发送到串行控制器的 i/o 控制。 通常情况下，客户端会向控制器发送 [**IOCTL \_ 串行 \_ 应用 \_ 默认 \_ 配置**](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_apply_default_configuration) 请求，将端口设置为其默认配置。 如有必要，客户端可以发送其他序列 IOCTLs 以替代一个或多个默认配置设置。 例如，Windows 定义了串行 IOCTLs 来更改波特率、流控制参数、行控制设置和读取和写入请求的超时值。 有关 SerCx2 支持的串行 IOCTLs 的列表，请参阅 [串行 I/o 请求接口](serial-i-o-request-interface.md)。