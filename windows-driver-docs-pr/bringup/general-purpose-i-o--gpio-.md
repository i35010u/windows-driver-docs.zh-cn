---
title: 常规用途 I/O (GPIO)
description: 芯片 (SoC) 集成线路上的系统地广泛使用的通用 I/O (GPIO) 插针。
ms.assetid: 9EB4EFC3-B94E-42C9-9FC7-12DF4AD01622
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: e1c1cbedf49fc95d184a60d8d4e093bbecf9ce06
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353974"
---
# <a name="general-purpose-io-gpio"></a>常规用途 I/O (GPIO)


芯片 (SoC) 集成线路上的系统地广泛使用的通用 I/O (GPIO) 插针。 对于基于 SoC 的平台，Windows 定义 GPIO 硬件常规抽象和这种抽象形式需要高级配置和电源接口 (ACPI) 命名空间的支持。

支持的 GPIO 抽象[ACPI 5.0 规范](https://uefi.org/specifications)这篇文章中列出的定义。

若要验证你的 GPIO 控制器是否满足所有 Windows 平台要求，请参阅[GPIO 控制器要求清单](gpio-controller-requirements-checklist.md)。

## <a name="gpio-controller-devices"></a>GPIO 控制器设备


Windows 支持 GPIO 控制器。 GPIO 控制器提供各种功能的外围设备，包括中断，输入信号，并输出信号。 GPIO 功能被建模为命名空间中的 GPIO 控制器设备。 [GPIO 框架扩展](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview)(GpioClx) 模型 GPIO 控制器设备作为分区到一定数量的银行的 pin。 每个 pin 银行有 64 或更少的可配置 pin。 银行公会 GPIO 控制器相对于他们的 pin 的位置相对于控制器的 GPIO 插针空间中进行排序。 例如，银行 0 包含在控制器上的 pin 0-31，银行 1 包含 pin 32 到 63 个，依次类推。 所有银行都具有相同数量的插针，可能都有较少的最后一个银行除外。 银行是，对于 ACPI 固件很重要，因为固件必须报告为银行、 系统中断资源的映射中所述**GPIO 命名空间对象**下面一节。

上一家银行的每个 pin 具有一组描述 pin 的配置方式的参数 （例如，输出、 级别区分中断、 取消退信的输入等）。

**GPIO 控制器和 ActiveBoth 中断**

一些 GPIO 控制器的一项功能是信号的能够生成中断 （上升，或 ActiveHigh 边缘和下降，或 ActiveLow 边缘） 这两个边缘上。 这可在各种应用程序，包括按钮界面，其中同时-按下按钮事件 (一个 edge) 中，按钮发布事件 （相反方向的边） 有意义。 此功能称为"ActiveBoth"。

在逻辑上，ActiveBoth 信号具有状态断言和 unasserted 状态，无论它们是瞬间断言 （例如，普通按钮），还是无限期长断言 （例如，耳机插孔插入）。 ActiveBoth 中断的边缘检测可能 GPIO 控制器硬件 （硬件 ActiveBoth） 中实现或 GPIO 驱动程序软件 (仿真 ActiveBoth) 来模拟。 Windows 要求实现 ActiveBoth GPIO 控制器必须使用模拟的 ActiveBoth。 这就需要确保可靠处理的所有方案不中断。 以 ActiveBoth 仿真，支持以下硬件要求适用：

1.  支持 ActiveBoth 中断的 GPIO 控制器必须支持级别模式中断，并且必须支持重新编程在运行时动态中断的极性。
2.  为了尽量减少 I/O 错误的风险，Windows 将优先使用而不是连接到存储的 GPIO 控制器内存映射 GPIO 控制器。 事实上，Windows 按钮数组设备 (PNP0C40) 中，需要它的 ActiveBoth GPIO 中断此设备连接到内存映射 GPIO 控制器，而不适用于连接存储的一个。 若要确定哪个按钮中断必须是 ActiveBoth，请参阅**按钮设备**sectionin[其他 ACPI 命名空间对象](other-acpi-namespace-objects.md)主题。
3.  若要建立 ActiveBoth 中断信号的确定性初始状态，Windows GPIO 设备堆栈可保证在驱动程序中断的连接将始终为信号的断言状态后生成的第一个中断。 堆栈进一步假定所有 ActiveBoth 中断线路的断言的状态逻辑级别较低 (ActiveLow edge) 默认情况下。 如果这不是你的平台上的情况，可通过包含 GPIO 控制器特定于设备的方法来替代默认 (\_DSM) 控制器的命名空间中。 有关此方法的详细信息，请参阅[GPIO 控制器特定于设备的方法 (\_DSM)](gpio-controller-device-specific-method---dsm-.md)。

> [!NOTE]
> 前面的列表中的第三个要求意味着使用 ActiveBoth 设备的驱动程序可能会收到初始化 （连接到） 后立即中断的中断，如果在 GPIO pin 信号在该时间是断言的状态。 这是可能的也适用于某些设备 （例如，头戴式耳机），甚至有可能，必须在驱动程序支持。

 

若要支持仿真的 ActiveBoth，GPIO 控制器驱动程序必须启用 （"选择中加入"） ActiveBoth 通过实现仿真[*客户端\_ReconfigureInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt)回调函数和设置**EmulateActiveBoth**标志中的基本信息结构的驱动程序的[*客户端\_QueryControllerBasicInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)回调函数提供给**GpioClx**。 有关详细信息，请参阅[常规用途 I/O (GPIO) 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/gpio)。

## <a name="gpio-namespace-objects"></a>GPIO 命名空间对象


GPIO 控制器和外围设备连接到它们，通过 ACPI 枚举。 使用 GPIO 连接资源描述符描述它们之间的连接。 有关详细信息，请参阅 ACPI 5.0 规范部分 6.4.3.8，"连接描述符"。

**设备标识和配置对象**

GPIO 控制器设备的 ACPI 名称空间包括以下组件：

-   供应商指派 ACPI 兼容的硬件 ID (\_HID) 对象。
-   使用的资源集 (\_CRS) 对象。
-   唯一 ID (\_UID) 对象，如果多个实例中的命名空间 （即，两个或多个命名空间节点具有相同的设备标识对象） 的 GPIO 控制器。

GPIO 控制器\_CRS 包含所有银行 GPIO 控制器中的所有使用的资源 （地址空间为寄存器、 系统中断等）。 中断资源银行映射表示在其中中断资源中列出的顺序\_CRS — 也就是说，列出的第一个中断分配给银行 0，列出的下一个分配银行 1，依次类推。 银行可以共享中断资源，此时中断一次为每个组连接到它，银行顺序列出和配置为共享。

**GPIO 连接资源描述符**

GPIO 连接资源描述符操作系统描述外围设备和连接到的 GPIO 插针之间的关系。 这些资源描述符可以定义两种类型的 GPIO 连接：GPIO 中断连接和 GPIO I/O 连接。 外围设备包括 GPIO 连接描述符中的其\_CRS 为所有 GPIO I/O 和中断插针连接。 如果连接的中断唤醒能够 (能够唤醒从低能耗空闲状态，则它必须配置为 ExclusiveAndWake 或 SharedAndWake; 有关详细信息，请参阅[设备电源管理](device-power-management.md)。

描述符节中定义 6.4.3.8.1，"GPIO 连接描述符"的 ACPI 5.0 规范。 这些描述符 ASL 资源模板宏部分所述 19.5.53，"GpioInt （GPIO 中断连接资源描述符宏）"的 ACPI 5.0 规范。

**GPIO 信号 ACPI 事件**

ACPI 定义允许硬件事件收到信号状态，传达给 ACPI 驱动程序在平台中的平台事件模型。 Windows 提供的服务进行通信的设备驱动程序的平台事件。 许多收件箱驱动程序依赖于此服务为 ACPI 定义的设备，如控制方法电源按钮、 合上盖子设备、 控制方法电池、 散热区等提供支持。 有关通知的详细信息，请参阅 ACPI 规范 5.6.5，"GPIO-Signaled ACPI 事件"部分。

对于 SoC 平台，GPIO 中断用于发出信号平台事件。 任何命名空间设备 （"ACPI 事件源"设备），用于通知事件到其使用 ASL 通知操作员的驱动程序需要以下项：

-   GPIO 控制器 ACPI 事件信号连接到的命名空间节点必须在其 ACPI 事件信息中包含该 pin 的 GpioInt 资源 (\_AEI) 对象 (请参阅部分 2.4.2.3.1，"ACPI 事件信息 (\_AEI) 对象", below)。 GpioInt 资源必须配置为非共享 （不含）。
-   控制器的节点必须还包含一条边 (\_Exx)、 级别 (\_Lxx) 或事件 (\_EVT) 控制方法对于中列出每个插针\_AEI 对象。

ACPI 驱动程序处理列出的 GPIO 中断，并为它的计算结果的边缘、 级别或事件的控制方法。 控制方法暂停硬件事件，如有必要，并在事件源设备的命名空间节点上执行所需的通知运算符。 然后，Windows 将通知发送到设备的驱动程序。 如果事件控制方法可以查询用于确定哪个事件发生的硬件，则可以通过同一 GpioInt 资源发出信号多个事件。 该方法然后必须通知的正确通知代码与正确的设备。

*ACPI 事件信息 (\_AEI) 对象*

如前文所述，GPIO 控制器的命名空间必须包含\_AEI 对象以便支持 ACPI 事件。 \_AEI 对象 （请参阅部分 5.6.5.2 ACPI 5.0 规范中） 返回包含此 GPIO 控制器通过 ACPI 事件发出信号的 GpioInt 描述符的资源模板缓冲区。 每个描述符对应于一个 ACPI 事件源设备，专用于该设备 （不共享设备之间）。

**GeneralPurposeIO 操作区域 (OpRegions)**

平台固件通常使用 GPIO 控制器以支持任意数量的平台的硬件功能，如控制电源和时钟，或在设备上设置模式。 若要支持从 ASL 控制方法使用 GPIO I/O，ACPI 5.0，请定义一个新的 OpRegion 类型，"GeneralPurposeIO"。

GPIO 控制器设备的驱动程序将处理 I/O 的命名空间范围内声明了 GeneralPurposeIO OpRegions （请参阅部分 5.5.2.4.4 ACPI 5.0 规范）。 GeneralPurposeIO 字段声明 （请参阅部分 5.5.2.4.4.1 ACPI 5.0 规范的） 将名称分配给要 GeneralPurposeIO OpRegion 内访问的 GPIO 插针。 GpioIO 连接资源 （请参阅部分 19.5.53 ACPI 5.0 规范） 中的字段声明中用于指定 pin 号码和特定的字段引用的配置。 总遵循连接描述符的已命名的字段比特数必须等于的描述符中列出的 pin 的数量。

可以声明命名空间中的任意位置并从该命名空间中的任何方法访问 OpRegion 中的字段。 对 GeneralPurposeIO OpRegion 访问的方向由第一次访问 （读取或写入），并且不能更改。

> [!NOTE]
> 因为 OpRegion 访问由 GPIO 控制器设备驱动程序 （"OpRegion 处理程序"），方法必须注意不要访问 OpRegion，直到有可用的驱动程序。 ASL 代码可以通过包括不同的区域来跟踪 OpRegion 处理程序的状态 (\_REG) GPIO 控制器设备 （请参阅部分 6.5.4 ACPI 5.0 规范的） 下的方法。 此外，OpRegion 依赖项 (\_DEP) 可在对象 （参见的 ACPI 5.0 规范部分 6.5.8） 下具有访问 GPIO OpRegion 字段的方法，如果所需的任何设备使用。 请参阅**设备依赖关系**主题中[设备管理命名空间对象](device-management-namespace-objects.md)有关何时使用的讨论主题\_dep。 非常重要的驱动程序不会分配也分配给 GeneralPurposeIO OpRegions 的 GPIO I/O 资源。 Opregions 是专供 ASL 控制方法。

 
