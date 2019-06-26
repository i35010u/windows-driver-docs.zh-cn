---
title: SerCx2.sys 和 Serial.sys 之间的差异
description: 尽管的收件箱 Sercx2.sys 和 Serial.sys 驱动程序组件这两个实现串行 I/O 请求接口，这些组件不能互换。 它们旨在满足不同的要求。
ms.assetid: 62FA69BB-FE04-4B5E-96CC-13764ED83AE6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a4a06a920869cddca280b91a00781054d4bf3a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366507"
---
# <a name="differences-between-sercx2sys-and-serialsys"></a>SerCx2.sys 和 Serial.sys 之间的差异


尽管的收件箱 Sercx2.sys 和 Serial.sys 驱动程序组件这两个实现[串行 I/O 请求接口](serial-i-o-request-interface.md)，这些组件不能互换。 它们旨在满足不同的要求。

**请注意**  Sercx2.sys 取代了早期版本的串行框架扩展，Sercx.sys，Windows 8 中引入的。 有关详细信息，请参阅[串行控制器驱动程序概述](serial-drivers-overview.md)。

 

## <a name="serialsys-dynamic-serial-connections-to-external-devices"></a>Serial.sys:动态与外部设备的串行连接


Serial.sys 旨在控制命名由 16550A 或类似 UARTs 驱动的 COM 端口。 可以动态插入和删除这些端口从外部外围设备。 Serial.sys 存在所有受支持版本的 Windows，并且许多现有的应用程序和使用 COM 端口的驱动程序依赖于 Serial.sys 的已知行为。 客户端按名称 (例如，"COM1") 打开 COM 端口，并在不再需要发布该端口。

Serial.sys 使用编程 I/O (PIO) 而不是 DMA 传输和通过串行端口接收数据。 使用 PIO 的主要原因是 PC 缺少合适的系统 DMA 控制器。 尽管 Serial.sys 可以用于控制串行端口 PCI 或 PCIe 串行适配器卡上，主要目的是控制 UARTs PC 母板上。 这些 UARTs 是从属没有内置主 DMA 控制器的设备。 从原理上讲，Serial.sys 可以使用系统的 DMA 控制器，但在 PC 时，此控制器是功能有限的 8237 设备。 实现多个串行端口，是多端口板可能包含主 DMA 控制器，但是看板的硬件供应商必须编写自定义串行驱动程序，能够利用这些 DMA 功能。

通过在 PC 上的 COM 端口的数据传输速度相对较慢，并可以由 PIO 充分处理。 可以从该处驱动 Serial.sys 由管理的 COM 端口的速度受到阻抗失和其他电气属性的连接器和外部将附加到这些端口的电缆。

## <a name="sercx2sys-dedicated-serial-connections-between-integrated-circuits"></a>Sercx2.sys:专用集成电路之间的串行连接


串行接口是现在广泛用于低 pin 计数之间提供通信集成电路上印刷电路板。 数据传输费率，通过这些接口可以是相对较高，因为较低的阻抗失和所涉及的短路径长度。 使用 PIO 若要将数据移到和从串行端口这些较高的数据速率过大带来了沉重负担处理器上。 相反，DMA 才可将此任务从处理器。

Sercx2.sys 旨在使用专用的串行端口的永久连接到外围设备和支持较高的数据速率。 与不同 Serial.sys，可以使 Sercx2.sys DMA 控制器在 SoC 基于硬件平台中的高级功能的使用。 这些 DMA 控制器可以执行很少或没有处理器干预的复杂数据传输。

Sercx2.sys 均提供所有版本的 Windows，从 Windows 8.1，但广泛应用于硬件平台的芯片 (SoC) 集成线路上包含系统和运行 Windows rt。 在这些平台 SoC 芯片包含 16550 D 或类似 UARTs 其串行端口连接到关闭芯片外围设备。 这些外围设备驻留在移动设备如智能手机或平板电脑计算机，这种情况，并且可能焊接到 SoC 芯片为相同的板。 作为此设备的驱动程序的专用的硬件资源分配永久连接到外围设备的串行端口。 通常情况下，驱动程序，并不是应用程序 — I/O 请求将直接发送到由 Sercx2.sys 和关联的串行控制器驱动程序管理的串行控制器。

Sercx2.sys 是灵活 DMA 支持。 完全支持使用系统 DMA 的复杂数据传输。 此外，Sercx2.sys 还提供可选的自定义传输模式，以支持，例如，具有内置的总线 master DMA 功能串行控制器。 最后，DMA 支持是可选的不需要实现串行控制器处理较低的数据费率 PIO 已足够。

## <a name="other-differences"></a>其他差异

由 Serial.sys 控制的 COM 端口分配的设备名称。 在用户模式应用程序可以打开此端口的名称，并将 I/O 请求直接发送到端口。

与此相反，由 SerCx2.sys 和串行控制器驱动程序控制的串行端口未命名。 拥有永久连接到端口外围设备的驱动程序收到特殊标识符 (称为[*连接 ID*](connection-ids-for-serially-connected-peripheral-devices.md)) 驱动程序使用打开的端口。 通常情况下，仅此外围设备的驱动程序可以直接向该端口发送的 I/O 请求。 需要可配置的端口，或将数据通过端口传输的应用程序将 I/O 请求发送到外围设备驱动程序。 然后，充当中介，该驱动程序的端口的发送相应的 I/O 请求。

Sercx2.sys 和其关联的串行控制器驱动程序启用运行时[电源管理框架](https://docs.microsoft.com/windows-hardware/drivers/kernel/overview-of-the-power-management-framework)(PoFx) 来管理能力和外围设备连接到这些控制器的串行控制器中。 PoFx，这是可从 Windows 8 开始，提供了细微调整的电源管理，若要启用移动设备上电池电量很长时间运行。

与此相反，Serial.sys 不受 PoFx，，而是依赖于 Windows 的早期版本中支持的设备电源管理功能。

另一个区别是，Serial.sys 实现软件流控制，但 Sercx2.sys 却没有。 Serial.sys 和 Sercx2.sys 支持硬件流控制使用*发送的请求*(RTS) 和*清除以发送*(CTS) 信号。 有关流控制的详细信息，请参阅[**串行\_HANDFLOW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ns-ntddser-_serial_handflow)。

最后一个区别是 Serial.sys 可以与 Serenum.sys，配合工作，但 Sercx2.sys 不能。 Serenum.sys 是枚举设备连接到串行端口的筛选器驱动程序。 有关详细信息，请参阅[枚举 Serenum 设备](enumerating-serenum-devices.md)。
