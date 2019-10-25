---
title: SerCx2.sys 和 Serial.sys 之间的差异
description: 尽管收件箱 Sercx2 驱动程序和 Serial 驱动程序组件都实现了串行 i/o 请求接口，但这些组件不能互换。 它们旨在满足不同的需求集。
ms.assetid: 62FA69BB-FE04-4B5E-96CC-13764ED83AE6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc6b0bb443d078725ec68b08998b476bcff08471
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845312"
---
# <a name="differences-between-sercx2sys-and-serialsys"></a>SerCx2.sys 和 Serial.sys 之间的差异


尽管收件箱 Sercx2 驱动程序和 Serial 驱动程序组件都实现了[串行 i/o 请求接口](serial-i-o-request-interface.md)，但这些组件不能互换。 它们旨在满足不同的需求集。

**请注意**  Sercx2 将替换 Windows 8 中引入的更早版本的串行 Framework 扩展 Sercx。 有关详细信息，请参阅[串行控制器驱动程序概述](serial-drivers-overview.md)。

 

## <a name="serialsys-dynamic-serial-connections-to-external-devices"></a>串行 .sys：到外部设备的动态串行连接


Serial 旨在控制由16550A 或类似 UARTs 驱动的命名 COM 端口。 外部外围设备可以动态地插入和删除这些端口。 Serial 在所有受支持的 Windows 版本中存在，并且许多使用 COM 端口的现有应用程序和驱动程序依赖于 Serial 的已知行为。 客户端按名称打开 COM 端口（例如 "COM1"），并在不再需要端口时释放该端口。

Serial 使用程控 i/o （PIO）而不是 DMA 来通过串行端口传输和接收数据。 使用 PIO 的主要原因是电脑缺少合适的系统 DMA 控制器。 尽管可以使用串行来控制 PCI 或 PCIe 串行适配器卡上的串行端口，但它主要用于控制 PC 主板上的 UARTs。 这些 UARTs 是没有内置 master DMA 控制器的从属设备。 原则上，Serial 可以使用系统 DMA 控制器，但是，在电脑中，此控制器是一种功能有限的8237设备。 多端口板实现多个串行端口，可能包含一个主 DMA 控制器，但该板的硬件供应商必须编写自定义串行驱动程序来利用这些 DMA 功能。

通过计算机上的 COM 端口进行的数据传输相对较慢，并且可以由 PIO 充分处理。 由 Serial 管理的 COM 端口可以驱动的速度受连接器的阻抗和其他电气属性和连接到这些端口的外部电缆的限制。

## <a name="sercx2sys-dedicated-serial-connections-between-integrated-circuits"></a>Sercx2：集成线路之间的专用串行连接


串行接口现在广泛用于在印刷电路板上的集成电路之间提供低针脚的通信。 由于少量的阻抗和短路径长度的影响，通过这些接口的数据传输速率可能会相对较高。 使用 PIO 将数据移入和移出这些高数据速率的串行端口会使处理器上的负担太大。 相反，需要使用 DMA 来从处理器卸载此工作。

Sercx2 专用于专用串行端口，这些端口永久连接到外围设备并支持高数据速率。 与 Sercx2 不同，可以利用基于 SoC 的硬件平台中 DMA 控制器的高级功能。 这些 DMA 控制器可以执行复杂的数据传输，只需很少或无需处理器干预。

Sercx2 在所有版本的 Windows 上都可用，从 Windows 8.1 开始，但在包含芯片（SoC）集成线路上的系统并运行 Windows RT 的硬件平台中广泛使用。 在这些平台中，SoC 芯片包含16550D 或类似的 UARTs，其串行端口连接到脱离芯片外围设备。 这些外围设备驻留在移动设备（如智能手机或平板电脑）的情况下，可能会焊接到与 SoC 芯片相同的板上。 永久连接到外围设备的串行端口被分配为此设备的驱动程序的专用硬件资源。 通常，只有驱动程序（而不是应用程序）将 i/o 请求直接发送到由 Sercx2 和关联串行控制器驱动程序管理的串行控制器。

Sercx2 对 DMA 的支持是灵活的。 完全支持使用系统 DMA 的复杂数据传输。 此外，Sercx2 还提供了一个可选的自定义传输模式来支持，例如，具有内置的 "总线主机" DMA 功能的串行控制器。 最后，DMA 支持是可选的，并且无需由串行控制器实现，该串行控制器处理 PIO 足够的数据速率。

## <a name="other-differences"></a>其他差异

为串行 .sys 控制的 COM 端口分配了设备名称。 用户模式应用程序可以按名称打开此端口，然后将 i/o 请求直接发送到端口。

相反，由 SerCx2 和串行控制器驱动程序控制的串行端口未命名。 拥有永久连接到端口的外围设备的驱动程序将收到一个特殊标识符（称为[*连接 ID*](connection-ids-for-serially-connected-peripheral-devices.md)），驱动程序将使用该标识符来打开端口。 通常，只有此外围设备驱动程序可以将 i/o 请求直接发送到端口。 需要配置端口或通过端口传输数据的应用程序会将 i/o 请求发送到外围设备驱动程序。 然后，该驱动程序作为中介，将相应的 i/o 请求发送到端口。

Sercx2 及其关联的串行控制器驱动程序允许运行时[电源管理框架](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)（PoFx）管理串行控制器和连接到这些控制器的外围设备中的电源。 PoFx （从 Windows 8 开始提供）提供了微调电源管理，使移动设备能够在电池电量上长时间运行。

与此相反，Serial 不由 PoFx 管理，而是依赖于 Windows 早期版本支持的设备电源管理功能。

另一个区别是，sys.databases 实现软件流控制，但 Sercx2 不实现。 Sys.databases 和 Sercx2 都支持使用*请求发送*（RTS）和*清除发送*（CTS）信号的硬件流控制。 有关流控制的详细信息，请参阅[**SERIAL\_HANDFLOW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_handflow)。

最后一个区别是，Serial 可以与 Serenum 结合使用，但 Sercx2 不能。 Serenum 是枚举连接到串行端口的设备的筛选器驱动程序。 有关详细信息，请参阅[枚举 Serenum 设备](enumerating-serenum-devices.md)。
