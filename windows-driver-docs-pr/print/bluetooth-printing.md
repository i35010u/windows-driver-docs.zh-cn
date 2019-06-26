---
title: 蓝牙打印
description: 蓝牙打印
ms.assetid: 6c40c142-9b52-4878-a84b-82d411086304
keywords:
- 打印机驱动程序 WDK、 蓝牙
- 蓝牙 WDK 打印
- 无线连接 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3717501c17b9048e51143806cc1247941a17f29
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384190"
---
# <a name="bluetooth-printing"></a>蓝牙打印


如果打印设备支持蓝牙，它应满足以下要求：

-   如果打印设备针对其 USB 或并行总线返回 1284 ID，蓝牙总线必须返回 1284 id。 如果出于[插](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)(PnP) 和标识、 设备返回 1284 ID 并行或 USB 总线上、 蓝牙总线还必须使用即插即用的标识的 1284 ID。
    **请注意**  并行或 USB 端口有永远不会拥有的设备仍应包含一个 1284 id。 而无需 1284 ID PnP 将不会创建打印队列。

     

-   设备应返回其 USB 或并行总线返回，以便 Microsoft Windows 操作系统可以正确标识设备，并不会将它与其他总线通过连接同一个设备混淆的同一个 1284 ID。 如果任何总线上的设备使用 1284 ID，应通过蓝牙返回相同的 ID。

    Windows 操作系统不使用 1284 ID 来跟踪多个总线通过附加的设备。 打印机应使用相同的 1284 ID，以便操作系统可以加载合适的驱动程序通过单一的 INF 条目。 打印机总线驱动程序，无需指定总线创建 PnP Id。 例如，Bluetooth 打印机获取窗体的应用 ID"BTHPRINT\\hpdeskje1234"和"hpdeskje1234"窗体。 第一种形式是特定于总线的第二个窗体与总线无关。 您可以创建 INF 使用任意一种 Id，具体取决于驱动程序包是否为完全总线无关。

-   设备必须支持蓝牙硬拷贝替换配置文件 (HCRP)。 对蓝牙 HCRP 的详细信息，请参阅[蓝牙网站](https://go.microsoft.com/fwlink/p/?linkid=26268)。
    **请注意**  ，Microsoft 才支持串行端口配置文件 (SPP)，但需要进行身份验证。 但是，我们建议而不是 SPP HCRP 因为 HCRP 提供更好的用户体验。

     

 

 




