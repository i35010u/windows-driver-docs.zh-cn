---
title: 常规用途 I/O (GPIO)
description: 芯片（SoC）集成线路上的系统广泛使用常规用途 i/o （GPIO） pin。
ms.assetid: 9EB4EFC3-B94E-42C9-9FC7-12DF4AD01622
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 38b0f118791afc1c5b7070ad4cc35bba99dd5d19
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834500"
---
# <a name="general-purpose-io-gpio"></a>常规用途 I/O (GPIO)


芯片（SoC）集成线路上的系统广泛使用常规用途 i/o （GPIO） pin。 对于基于 SoC 的平台，Windows 定义了 GPIO 硬件的常规抽象，此抽象需要高级配置和电源接口（ACPI）命名空间中的支持。

本文中列出的[ACPI 5.0 规范](https://uefi.org/specifications)定义支持 GPIO 抽象。

若要验证 GPIO 控制器是否满足所有 Windows 平台要求，请参阅[GPIO 控制器要求清单](gpio-controller-requirements-checklist.md)。

## <a name="gpio-controller-devices"></a>GPIO 控制器设备


Windows 支持 GPIO 控制器。 GPIO 控制器为外围设备提供各种功能，包括中断、输入信号和输出信号。 GPIO 功能作为命名空间中的 GPIO 控制器设备建模。 [Gpio framework 扩展](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview)（GpioClx）将 gpio 控制器设备建模为某个数量的 pin 的分区。 每个 pin bank 具有64或更少的可配置 pin。 GPIO 控制器中的银行相对于控制器在控制器的 GPIO 固定空间内的位置进行排序。 例如，bank 0 在控制器上包含引脚0-31，bank 1 包含引脚32-63，依此类推。 除最后一个银行以外，所有的银行都具有相同数量的 pin，这可能更少。 银行对于 ACPI 固件非常重要，因为固件必须报告系统中断资源到银行的映射，如下面的**GPIO 命名空间对象**部分所述。

银行上的每个 pin 都具有一组用于描述如何配置 pin 的参数（例如，输出、区分级别的中断、被退回的输入等）。

**GPIO 控制器和 ActiveBoth 中断**

某些 GPIO 控制器的一项功能是能够在信号边缘（上升、ActiveHigh 边缘、下降或 ActiveLow 边缘）上生成中断。 这在各种应用程序（包括按钮界面）中非常有用，在这种情况下，按钮-按下事件（一个边缘）和按钮释放事件（相反边缘）都有意义。 此功能称为 "ActiveBoth"。

从逻辑上讲，ActiveBoth 信号具有已断言和 unasserted 的状态，无论它们是暂时断言（例如，普通按钮），还是无限长的断言（例如耳机插孔插入）。 ActiveBoth 中断的边缘检测可能在 GPIO 控制器硬件（硬件 ActiveBoth）中实现，或在 GPIO 驱动程序软件（模拟 ActiveBoth）中进行模拟。 Windows 要求实现 ActiveBoth 的 GPIO 控制器必须使用模拟 ActiveBoth。 这是为了确保在所有情况下都能可靠地处理双重边缘中断。 为了支持 ActiveBoth 仿真，需要满足以下硬件要求：

1.  支持 ActiveBoth 中断的 GPIO 控制器必须支持级别模式中断，并且必须支持在运行时动态地重新对中断的极性进行编程。
2.  为了最大限度地降低 i/o 错误的风险，Windows 首选使用内存映射的 GPIO 控制器，而不是使用 SPB 连接的 GPIO 控制器。 事实上，对于 Windows 按钮阵列设备（PNP0C40），需要将此设备的 ActiveBoth GPIO 中断连接到内存映射的 GPIO 控制器，而不是连接到 SPB 连接的控制器。 若要确定哪些按钮中断必须 ActiveBoth，请参阅 "**设备**SECTIONIN[其他 ACPI 命名空间对象](other-acpi-namespace-objects.md)" 主题。
3.  若要为 ActiveBoth 中断信号建立确定的初始状态，Windows GPIO 设备堆栈可保证驱动程序中断连接后生成的第一个中断始终为信号的断言状态。 堆栈进一步假设默认情况下，所有 ActiveBoth 中断线路的断言状态都为逻辑级别 low （ActiveLow 边缘）。 如果在平台上不是这样，则可以通过在控制器的命名空间中包含 GPIO 控制器设备特定的方法（\_DSM）来覆盖默认值。 有关此方法的详细信息，请参阅[GPIO 控制器设备特定方法（\_DSM）](gpio-controller-device-specific-method---dsm-.md)。

> [!NOTE]
> 前面的列表中的第三项要求表明，使用 ActiveBoth 的设备的驱动程序可能会在初始化（连接到）中断后立即收到中断，前提是 GPIO pin 上的信号在此时处于已断言状态。 这是可能的，甚至可能是某些设备（例如耳机），并且必须在驱动程序中受支持。

 

若要支持模拟的 ActiveBoth，GPIO 控制器驱动程序必须启用（"选择加入"） ActiveBoth 仿真，方法是实现一个\_ReconfigureInterrupt 回调**函数的**[*客户端*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt)，并在基本驱动程序的[*客户端\_QueryControllerBasicInformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)回调函数向**GpioClx**提供的信息结构。 有关详细信息，请参阅[常规用途 i/o （GPIO）驱动程序](https://docs.microsoft.com/windows-hardware/drivers/gpio)。

## <a name="gpio-namespace-objects"></a>GPIO 命名空间对象


GPIO 控制器和连接到它们的外围设备由 ACPI 枚举。 使用 GPIO 连接资源描述符描述它们之间的连接。 有关详细信息，请参阅 ACPI 5.0 规范的 "连接描述符" 一节。

**设备标识和配置对象**

GPIO 控制器设备的 ACPI 命名空间包括以下各项：

-   供应商分配的符合 ACPI 的硬件 ID （\_HID）对象。
-   使用的一组资源（\_CRS）对象。
-   唯一 ID （\_UID）对象，如果命名空间中有多个 GPIO 控制器实例（即，具有相同设备标识对象的两个或多个命名空间节点）。

GPIO 控制器的 \_CRS 包含 GPIO 控制器中所有银行使用的所有资源（寄存器、系统中断等的地址空间）。 中断资源到银行的映射按照 \_CRS 中列出中断资源的顺序来表示，即，列出的第一个中断分配给 bank 0，下一个列出的将分配给 bank 1，依此类推。 银行可以共享中断资源，在这种情况下，对于每个连接到它的银行，按 bank order 列出中断，并将其配置为共享。

**GPIO 连接资源描述符**

外围网络与它们所连接的 GPIO 引脚之间的关系将通过 GPIO 连接资源描述符描述为操作系统。 这些资源描述符可以定义两种类型的 GPIO 连接： GPIO 中断连接和 GPIO i/o 连接。 外围设备包括其 \_CRS 中的 GPIO 连接描述符，适用于所有已连接的 GPIO i/o 和中断 pin。 如果连接的中断支持唤醒（能够从低功耗空闲状态唤醒系统，则必须将其配置为 ExclusiveAndWake 或 SharedAndWake; 有关详细信息，请参阅[设备电源管理](device-power-management.md)。

这些描述符在 ACPI 5.0 规范的 "GPIO 连接描述符" 部分中定义。 ACPI 5.0 规范的 "GpioInt （GPIO 中断连接资源描述符宏）" 一节中介绍了这些描述符的 ASL 资源模板宏。

**GPIO-已发出 ACPI 事件**

ACPI 定义了平台事件模型，使平台中的硬件事件可以发出信号并传达给 ACPI 驱动程序。 Windows 提供了通知服务，用于将平台事件传递到设备驱动程序。 许多收件箱驱动程序依赖于此服务来为 ACPI 定义的设备提供支持，如控制方法电源按钮、盖子设备、控制方法电池、热区等。 有关通知的详细信息，请参阅 ACPI 规范的 "5.6.5" 部分。

对于 SoC 平台，GPIO 中断用于向平台事件发出信号。 使用 ASL 通知运算符向其驱动程序发出事件的任何命名空间设备（"ACPI 事件源" 设备）都需要以下各项：

-   ACPI 事件信号所连接的 GPIO 控制器的 namespace 节点必须在其 ACPI 事件信息（\_AEI）对象中包含该 pin 的 GpioInt 资源（请参阅下面的 "ACPI 事件信息（\_AEI）对象" 部分2.4.2.3.1）。 GpioInt 资源必须配置为非共享（独占）。
-   控制器的节点还必须包含 \_AEI 对象中列出的每个 pin 的边缘（\_Exx）、级别（\_Lxx）或事件（\_.EVT）控制方法。

ACPI 驱动程序处理列出的 GPIO 中断，并为其计算边缘、级别或事件控制方法。 如有必要，控制方法 quiesces 硬件事件，并在事件源设备的命名空间节点上执行所需的通知运算符。 然后，Windows 将通知发送到设备的驱动程序。 如果事件控制方法可以查询硬件来确定发生了哪种事件，则可以通过相同的 GpioInt 资源对多个事件发出信号。 然后，该方法必须将正确的通知代码通知正确的设备。

*ACPI 事件信息（\_AEI）对象*

如前文所述，GPIO 控制器的命名空间必须包含 \_AEI 对象才能支持 ACPI 事件。 \_AEI 对象（请参阅 ACPI 5.0 规范中的 "5.6.5.2" 部分）返回一个资源模板缓冲区，该缓冲区只包含通过此 GPIO 控制器对 ACPI 事件发出信号的 GpioInt 描述符。 每个描述符对应于一个 ACPI 事件源设备，并专用于该设备（不在设备之间共享）。

**GeneralPurposeIO 操作区域（OpRegions）**

平台固件通常使用 GPIO 控制器来支持任意数量的平台硬件功能，如控制电源和时钟，或在设备上设置模式。 若要支持从 ASL 控制方法使用 GPIO i/o，ACPI 5.0 定义了新的 OpRegion 类型 "GeneralPurposeIO"。

GeneralPurposeIO OpRegions （请参阅 ACPI 5.0 规范的部分5.5.2.4.4）是在 GPIO 控制器设备的命名空间范围内声明的，驱动程序将处理 i/o。 GeneralPurposeIO 字段声明（请参阅 ACPI 5.0 规范的部分5.5.2.4.4.1）将名称分配给将在 GeneralPurposeIO OpRegion 内访问的 GPIO pin。 GpioIO 连接资源（请参阅 ACPI 5.0 规范的部分19.5.53）用于指定特定字段引用的 pin 号和配置。 连接描述符后的命名字段位的总数必须等于描述符中列出的 pin 数目。

OpRegion 中的字段可以在命名空间中的任何位置进行声明，并可从命名空间中的任何方法进行访问。 对 GeneralPurposeIO OpRegion 的访问方向由第一次访问（读取或写入）决定，无法更改。

> [!NOTE]
> 由于 GPIO 控制器设备驱动程序（"OpRegion 处理程序"）提供 OpRegion 访问，因此，在该驱动程序可用之前，方法必须注意不要访问 OpRegion。 ASL 代码可以通过在 GPIO 控制器设备下包含区域（\_REG）方法来跟踪 OpRegion 处理程序的状态（请参阅 ACPI 5.0 规范的6.5.4 部分）。 此外，如果需要，可以在具有访问 GPIO OpRegion 字段的方法的任何设备下使用 OpRegion 依赖项（\_DEP）对象（请参阅 ACPI 5.0 规范的6.5.8 部分）。 有关何时使用 \_DEP 的讨论，请参阅[设备管理命名空间对象](device-management-namespace-objects.md)主题中的**设备依赖项**部分。 不会为驱动程序分配 GPIO i/o 资源（这些资源也分配给 GeneralPurposeIO OpRegions），这一点很重要。 Opregions 用于独占使用 ASL 控制方法。

 
