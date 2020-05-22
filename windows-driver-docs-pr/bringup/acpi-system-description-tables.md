---
title: ACPI 系统说明表
description: 在基于 SoC 的平台上不需要实现高级配置和电源接口（ACPI）硬件规范，但很多 ACPI 软件规范都是必需的。
ms.assetid: 6EFCD288-031D-46BB-ABF3-8ADB53E7B4B1
ms.date: 05/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 81c9481b1717eb8972a85367f6884ef05bcdc678
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769389"
---
# <a name="acpi-system-description-tables"></a>ACPI 系统说明表

在基于 SoC 的平台上不需要实现高级配置和电源接口（ACPI）硬件规范，但很多 ACPI 软件规范都是必需的。 ACPI 定义了一个通用的可扩展表传递机制，还定义了用于为操作系统描述平台的特定表。

在[ACPI 5.0 规范](https://uefi.org/specifications)中定义表结构和标头，包括 ID 和校验和字段。 除了本文中所述的特定表，Windows 还利用此表传递机制。

这些表的原理是使通用软件支持可通过多种方式集成到各种平台的标准知识产权（IP）块。 使用表策略时，特定平台的平台变量属性在表中提供，由通用软件用于将自身调整为集成到平台中的特定 IP 块集。 因此，此软件可以写入一次，经过全面测试，然后在一段时间内优化。

## <a name="root-system-description-pointer-rsdp"></a>根系统说明指针（RSDP）

Windows 依赖于 UEFI 固件启动硬件平台。 因此，Windows 将使用 EFI 系统表来查找 RSDP，如[ACPI 5.0 规范](https://uefi.org/specifications)的 "查找启用了 UEFI 的 RSDP" 一节中所述。 平台固件会填写 RSDP 中 RSDT 或 XSDT 的地址。 （如果同时提供了这两个表地址，则 Windows 将更倾向于 XSDT。）

## <a name="root-system-description-table-rsdt"></a>根系统说明表（RSDT）

RSDT （或 XSDT）包含指向平台上提供的任何其他系统说明表的指针。 具体而言，此表包含指向以下内容的指针：

- 固定 ACPI 硬件表（FADT）

- 多个中断控制器表（MADT）

- （可选）核心系统资源表（CSRT）

- 调试端口表2（DBG2）

- 启动图形资源表（BGRT）

- 固件性能数据表（FPDT）

- 基本系统描述表（DSDT）

- （可选）其他系统说明表（SSDT）

## <a name="fixed-acpi-description-table-fadt"></a>固定 ACPI 说明表（FADT）

固定 ACPI 硬件表（FADT）包含有关平台上可用的各种固定硬件功能的重要信息。 为了支持硬件缩减的 ACPI 平台，ACPI 5.0 扩展了 FADT 表的定义，如下所示：

- FADT （偏移量为112）中的 "标志" 字段有两个新标志：

    硬件 \_ 降低了 \_ ACPI 位偏移量20。 指示 ACPI 硬件在此平台上不可用。 如果未实现 ACPI 固定硬件编程模型，则必须设置此标志。

    低 \_ 功耗 \_ S0 \_ 空闲 \_ 支持位偏移量21。 指示该平台支持 ACPI S0 系统电源状态内的低功耗空闲状态，比任何 Sx 睡眠状态更节能。 如果设置了此标志，则 Windows 将不会尝试睡眠和恢复，但会改用平台空闲状态和连接备用。

- FADT 首选 \_ PM \_ 配置文件字段（字节偏移量45）有一个新的角色条目 "绘图板"。 此角色会影响显示和输入的电源管理策略，并影响屏幕键盘的显示。
- "IA-PC 引导体系结构标志" 字段（偏移量为109）有一个新的 "CMOS RTC 不存在" 标志（位偏移量5），表示未实现 PC 的 CMOS RTC，或在旧地址中不存在。 如果设置了此标志，则平台必须实现 ACPI 时间和警报控制方法设备。 有关详细信息，请参阅[ACPI 定义的设备](acpi-defined-devices.md)主题中的**控制方法时间和警报设备**部分。
- 添加了新的字段，以支持在硬件上减少了 ACPI 平台上的传统 PC 睡眠/恢复。 这些字段将被 Windows 忽略，但在表中必须存在才能遵从符合性。
- 如果设置了硬件 \_ 缩减了 \_ acpi 标志，操作系统将忽略与 ACPI 硬件规范相关的所有字段。

所有其他 FADT 设置将保留它们在以前版本的 ACPI 4.0 中的含义。 有关详细信息，请参阅[ACPI 5.0 规范](https://uefi.org/specifications)的 "固定 Acpi 说明表（FADT）" 5.2.9 部分。

## <a name="multiple-apic-description-table-madt"></a>多个 APIC 说明表（MADT）

在 ACPI 的 PC 实现中，将使用多个 APIC 说明表（MADT）和特定于 PC 的中断控制器描述符来描述系统中断模式。 对于基于 ARM 的 SoC 平台，ACPI 5.0 添加了 ARM 控股通用中断控制器（GIC）和 GIC 分发服务器的描述符。 Windows 包括对 GIC 和 GIC 分发服务器的收件箱支持。 有关这些描述符的详细信息，请参阅[ACPI 5.0 规范](https://uefi.org/specifications)的节5.2.12.14、"GIC 结构" 和 5.2.12.15 "GIC 分发服务器结构"。

中断控制器描述符结构紧跟在 MADT 中的 "标志" 字段之后。 对于 ARM 平台，每个 GIC 列出一个描述符，后跟每个 GIC 分发服务器的一个。 与启动处理器相对应的 GIC 必须为中断控制器描述符列表中的第一项。

## <a name="generic-timer-description-table-gtdt"></a>一般计时器说明表（GTDT）

与中断控制器一样，ACPI 中有一个标准的计时器说明表。 对于使用 GIT 计时器的 ARM 系统，可使用 ACPI 的 GTDT 在 Windows 中利用对 GIT 的内置支持。

## <a name="core-system-resources-table-csrt"></a>核心系统资源表（CSRT）

核心系统资源（Csr）是共享的硬件功能，如中断控制器、计时器和 DMA 控制器（操作系统必须将其序列化到此类）。 对于定时器和中断控制器等功能（在 x86 体系结构和 ARM 体系结构上）的行业标准，Windows 基于 ACPI （例如 MADT 和 GTDT）中所述的标准表为这些功能提供支持。 但是，在行业聚合 DMA 控制器接口标准之前，需要在操作系统中支持某些非标准设备。

Windows 支持 HAL 扩展的概念以解决此问题。 HAL 扩展是以 Dll 形式实现的 SoC 特定模块，可将 Windows HAL 改编为 Windows 所需的特定 CSR 类的特定硬件接口。 为了识别并加载这些非标准 CSR 模块，Microsoft 定义了一个新的 ACPI 表。 如果在平台上使用了非标准 Csr，此表（在 ACPI 规范中具有 "CSRT" 的保留签名）必须包含在 RSDT 中。

CSRT 描述 Csr 的资源组，其中每个资源组标识特定类型的硬件。 Windows 使用为资源组提供的标识符来查找并加载此组所需的 HAL 扩展。 CSRT 中的资源组还可能包含单个资源描述符，具体取决于 CSR 类型和 HAL 扩展的需要。 这些资源描述符的格式和使用由 HAL 扩展写入器定义，用户可以通过更改 CSRT 中包含的资源描述符，使扩展更易于移植，从而支持各种不同的 SoC 平台。

为了支持维护 HAL 扩展，并管理这些扩展使用的系统资源，CSRT 中描述的每个资源组也必须在平台的 ACPI 命名空间中表示为一个设备。 有关详细信息，请参阅以下 "区分系统描述表（DSDT）" 部分。 资源组标头中使用的设备标识符必须与设备的命名空间节点中使用的标识符匹配。 有关详细信息，请参阅[设备管理命名空间对象](device-management-namespace-objects.md)主题中的 " **ACPI 中的设备标识**" 部分。 存在这些资源组命名空间设备后，可通过 Windows 更新服务提供 HAL 扩展。

有关详细信息，请参阅[核心系统资源表（CSRT）规范](https://acpica.org/related-documents)。

## <a name="debug-port-table-2-dbg2"></a>调试端口表2（DBG2）

Microsoft 需要在所有系统上都有调试端口。 为了描述内置于平台中的调试端口，Microsoft 定义了用于 ACPI 的调试端口表2（DBG2）。 此表指定一个或多个独立端口用于调试目的。 如果存在 DBG2 表，则指示该平台至少包含一个调试端口。 此表包含有关调试端口的标识和配置的信息。 该表位于具有其他 ACPI 表的系统内存中，并且必须在 ACPI RSDT 表中进行引用。

Windows 使用 DBG2 表中的端口类型值来标识和加载系统需要的内核调试器（KD）传输（例如，USB 或串行）。 然后，KD 传输使用 DBG2 表中的端口子类型值来标识端口使用的硬件接口。 DBG2 表中的其他信息指定端口寄存器的系统地址，该地址由硬件接口模块用于指定的子类型。 最后，DBG2 表必须包括对与调试端口对应的 ACPI 命名空间中的设备节点的引用。 此引用使 Windows 能够管理调试使用情况和设备的正常使用情况之间的冲突（如果有），还可将调试器与电源转换集成。

有关详细信息，请参阅[Microsoft 调试端口表2（DBG2）规范](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn639131(v=vs.85))。

## <a name="differentiated-system-description-table-dsdt"></a>差分系统说明表（DSDT）

在 ACPI 中，平台上的外围设备和系统硬件功能在启动时加载或在启动时加载或在运行时动态加载的辅助系统说明表（DSDT）中进行了介绍。 对于 Soc，平台配置通常是静态的，因此 DSDT 可能已足够，尽管 Ssdt 还可用于改进平台说明的模块化。

ACPI 定义了一种解释型语言（ACPI 源语言或 ASL）和执行环境（ACPI 虚拟机），用于描述系统设备和功能及其平台特定的控件，以与 OS 无关的方式进行说明。 ASL 用于定义 ACPI 命名空间中的命名对象， [MICROSOFT ASL 编译器](microsoft-asl-compiler.md)用于生成 acpi 机器语言（AML）字节代码，用于传输到 DSDT 中的操作系统。 收件箱[WINDOWS acpi 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)SYS.DATABASES 实现 acpi 虚拟机，并解释 AML 字节代码。 AML 对象可能只返回说明信息。 或者，AML 对象可能是执行计算或执行 i/o 操作的方法。 *控制方法*是一个可执行的 AML 对象，它使用操作系统的设备驱动程序在平台硬件上执行 i/o 操作。 ASL 使用 OpRegions 来抽象操作系统中可访问的各种地址空间。 控制方法执行 i/o 操作，作为与 OpRegions 中声明的命名字段进行的一系列传输。

有关 OpRegions 的详细信息，请参阅[ACPI 5.0 规范](https://uefi.org/specifications)中的 "访问操作区域" 部分。 有关 ASL 和控制方法的详细信息，请参阅 ACPI 5.0 规范中的第5.5 节 "ACPI 命名空间"。

Windows 提供对开发和调试 ASL 代码的支持。 ASL 编译器包含一个拆装器，使实施者能够从调试目标加载命名空间。 然后，可以使用 ASL 编译器将命名空间重新应用于目标以实现快速原型制作和测试，而无需闪现系统固件。 此外，Windows 内核调试器和 Acpi .sys 驱动程序的已检查（.CHK）版本支持跟踪和分析 AML 执行。 有关详细信息，请参阅[AMLI 调试器](https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction-to-the-amli-debugger)。

## <a name="windows-smm-security-mitigations-table-wsmt"></a>Windows SMM 安全缓解表（WSMT）

Windows SMM 安全缓解表 (WSMT) 规范包含高级配置和电源接口 (ACPI) 表的详细信息，创建的 ACPI 表供支持 Windows 基于虚拟化的安全性 (VBS) 功能的 Windows 操作系统使用。

此信息适用于以下操作系统：

Windows Server 2016

Windows 10 版本 1607

有关详细信息，请参阅[WINDOWS SMM 安全缓解表（WSMT）规范](https://go.microsoft.com/fwlink/p/?LinkId=786943)。
