---
title: ACPI 系统说明表
description: 基于 SoC 的平台上不需要高级配置和电源接口 (ACPI) 硬件规范的实现，但许多 ACPI 软件规范是 （或可以） 所需。
ms.assetid: 6EFCD288-031D-46BB-ABF3-8ADB53E7B4B1
ms.date: 07/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8392a2f25f3a62be193cfd93bb62d9c4bc9f27a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328113"
---
# <a name="acpi-system-description-tables"></a>ACPI 系统说明表


基于 SoC 的平台上不需要高级配置和电源接口 (ACPI) 硬件规范的实现，但许多 ACPI 软件规范是 （或可以） 所需。 ACPI 定义泛型、 可扩展的表传递机制，以及用于描述对操作系统的平台特定的表。

中定义的表结构和标头，包括 ID 和校验和字段[ACPI 5.0 规范](https://www.uefi.org/specifications)。 Windows 使用此表传递机制，除了本文中介绍的特定表。

这些表背后的理念是要启用要支持标准的知识产权 (IP) 块，可以通过不同的方式集成到各种平台的通用软件。 通过表策略，在特定平台的平台变量属性在表中，提供和通用软件使用自己以适应特定的一组集成到平台中的 IP 块。 此软件可以因此和中写入一次，全面测试，然后随着时间的推移进行优化。

## <a name="root-system-description-pointer-rsdp"></a>根系统说明指针 (RSDP)


Windows 取决于硬件平台上才能启动的 UEFI 固件。 因此，Windows 将使用 EFI 系统表来查找 RSDP 的一部分 5.2.5.2，"查找 RSDP 上 UEFI 启用系统"中, 所述[ACPI 5.0 规范](https://www.uefi.org/specifications)。 平台固件填充 RSDT 或 xsdt 表 RSDP 中的地址。 （如果提供了这两个表地址，Windows 将首选 xsdt 表。 )

## <a name="root-system-description-table-rsdt"></a>根系统描述表 (RSDT)


RSDT 或 xsdt 表） 包含在平台上提供任何其他系统描述表的指针。 具体而言，此表包含指向以下：

-   固定的 ACPI 硬件表 (FADT)
-   多个中断控制器表 (MADT)
-   （可选） 在核心系统资源表 (CSRT)
-   调试端口表 2 (DBG2)
-   启动图形资源表 (BGRT)
-   固件性能数据表 (FPDT)
-   基本系统描述表 (DSDT)
-   （可选） 其他系统描述表 (SSDT)

## <a name="fixed-acpi-description-table-fadt"></a>固定的 ACPI 描述表 (FADT)


固定 ACPI 硬件表 (FADT) 包含在平台上提供的各种固定硬件功能的重要信息。 若要支持硬件减少 ACPI 平台，ACPI 5.0 扩展 FADT 表定义，如下所示：

-   FADT （偏移量 112） 中的标志字段具有两个新标记：

    硬件\_减少了\_ACPI 位偏移量的 20。 指示 ACPI 硬件不在此平台上可用。 如果未实现 ACPI 固定硬件编程模型，必须设置此标志。

    低\_电源\_S0\_空闲\_能够位偏移量 21。 指示该平台支持低能耗空闲状态中的 ACPI S0 系统电源状态的更高的能效比任何 Sx 睡眠状态。 如果设置此标志，Windows 将尝试进入睡眠状态并继续，但将改为使用平台空闲状态和连接待机状态。

-   FADT 首选\_PM\_配置文件字段 （的字节偏移量 45） 都有一个新的角色项"平板电脑"。 此角色会影响用于显示和输入，电源管理策略，并会影响显示屏幕键盘。
-   "IA PC 启动体系结构标志"字段 （偏移量 109） 都有一个新的"CMOS RTC 不存在"标志 （位偏移量 5） 以指示 PC 的 CMOS RTC 要么未实现，或在旧地址中不存在。 如果设置此标志，该平台必须实现 ACPI 时间和警报控件方法设备。 有关详细信息，请参阅**控制方法时间和警报的设备**主题中[ACPI 定义设备](acpi-defined-devices.md)主题。
-   添加新字段以支持硬件减少 ACPI 平台上的传统 PC 睡眠/恢复。 这些字段将忽略由 Windows，但必须存在的表中的符合性。
-   如果硬件\_减少了\_ACPI 标志设置，则操作系统会忽略与 ACPI 硬件规范相关的所有字段。

所有其他 FADT 设置保留从以前的版本，其含义 ACPI 4.0。 有关详细信息，请参阅 》 的部分第 5.2.9 节，"固定 ACPI 描述表 (FADT)"， [ACPI 5.0 规范](https://www.uefi.org/specifications)。

## <a name="multiple-apic-description-table-madt"></a>多个 APIC 说明表 (MADT)


在 PC 实现中的 ACPI、 多个 APIC 说明表 (MADT) 和特定于 PC 的使用中断控制器描述符来描述系统中断模型。 对于基于 ARM 的 SoC 平台，ACPI 5.0 将描述符添加 ARM Holdings' 泛型中断控制器 (GIC) 和 GIC 分发服务器。 Windows 包括对 GIC 和 GIC 分发服务器的收件箱支持。 有关这些描述符的详细信息，请参阅节 5.2.12.14、"GIC 结构"和 5.2.12.15，"GIC 分发服务器结构"的[ACPI 5.0 规范](https://www.uefi.org/specifications)。

紧跟在 MADT 标志字段中列出了中断控制器描述符结构。 对于 ARM 平台，一个描述符列出的每个 GIC 后, 跟另一个用于每个 GIC 分发服务器。 对应于启动处理器 GIC 必须中断控制器描述符的列表中的第一个条目。

## <a name="generic-timer-description-table-gtdt"></a>泛型计时器说明表 (GTDT)


与中断控制器中，ACPI 中没有标准计时器说明表。 对于利用 GIT 计时器的 ARM 系统，可以使用 ACPI 的 GTDT 利用 Windows 中的 GIT 的内置支持。

## <a name="core-system-resources-table-csrt"></a>内核系统资源表 (CSRT)


核心系统资源 (Csr) 位于共享的硬件功能，如中断控制器、 计时器和 DMA 控制器到的操作系统必须序列化的访问。 行业标准存在计时器之类的功能和中断控制器 （在 x86 和 ARM 体系结构），其中 Windows 构建基于 ACPI （例如，MADT 和 GTDT） 中所述的标准表这些功能的支持。 但是，直到行业收敛 DMA 控制器接口标准，是需要在操作系统中支持一些非标准的设备。

Windows 支持 HAL 扩展来解决此问题的概念。 HAL 扩展是特定于 SoC 的模块，作为 Dll，调整 Windows HAL 到 CSR Windows 所需的特定类的特定硬件接口实现。 为了标识和加载这些非标准的 CSR 模块，Microsoft 还定义了一个新的 ACPI 表。 具有"CSRT"ACPI 规范中的保留的签名，此表必须包含 RSDT 中，如果在平台上使用了非标准的 Csr。

CSRT 介绍 Csr，其中每个资源组标识的特定类型的硬件的资源的组。 Windows 使用提供的资源组的标识符来查找并加载所需的 HAL 扩展名为此组。 CSRT 中的资源组还可能包含单个资源描述符，具体取决于 CSR 类型和 HAL 扩展的需求。 HAL 扩展编写器，可以使扩展得更易于移植，从而支持各种不同的 SoC 平台只需通过更改 CSRT 中包含资源描述符由定义的格式和使用这些资源描述符。

若要支持的 HAL 扩展维护并管理使用这些扩展的系统资源，CSRT 中所述的每个资源组必须还将表示为设备平台的 ACPI 命名空间内。 有关详细信息，请参阅下面的"区分系统说明表 (DSDT)"部分。 使用资源组标头中的设备标识符必须与在设备的命名空间节点中使用的标识符匹配。 有关详细信息，请参阅**ACPI 中的设备标识**主题中[设备管理命名空间对象](device-management-namespace-objects.md)主题。 这些资源组命名空间的设备存在允许 HAL 扩展 Windows 更新服务提供服务。

有关详细信息，请参阅[核心系统资源表 (CSRT) 规范](http://acpica.org/related-documents)。

## <a name="debug-port-table-2-dbg2"></a>调试端口表 2 (DBG2)


Microsoft 需要在所有系统上的调试端口。 若要描述平台中内置的调试端口，Microsoft 定义的 ACPI 的调试端口表 2 (DBG2)。 此表指定一个或多个独立端口以便进行调试。 DBG2 表的存在表明该平台包括至少一个调试端口。 此表包含有关标识和调试端口的配置信息。 表位于其他 ACPI 表中，在系统内存中，必须在 ACPI RSDT 表中引用。

Windows DBG2 表中使用的端口类型值来标识和加载的 Kernel Debugger (KD) 传输 （例如，USB 或序列） 的系统要求。 KD 传输然后使用端口子类型值中 DBG2 表来标识该端口所使用的硬件接口。 DBG2 表中的其他信息指定端口寄存器中，由指定的子类型的硬件接口模块的系统地址。 最后，DBG2 表必须包含对应于调试端口的 ACPI 命名空间中的设备节点的引用。 此参考，Windows 管理调试使用和正常使用的设备，如果有的话之间的冲突以及将调试器与电源转换相集成。

有关详细信息，请参阅[Microsoft 调试端口表 2 (DBG2) 规范](https://go.microsoft.com/fwlink/p/?linkid=330996)。

## <a name="differentiated-system-description-table-dsdt"></a>差异化的系统描述表 (DSDT)


在不同的系统说明表 (DSDT)，它在启动加载，或辅助系统说明表 (Ssdt) 在启动加载或动态加载中 ACPI，外围设备和平台上的系统硬件功能所述在运行时。 有关 Soc，平台配置是通常是静态的因此 DSDT 可能就足够了，尽管 Ssdt 还可以用来提高平台说明的模块化。

ACPI 定义用于描述系统的设备和功能，以及其特定于平台的控件，OS 不可知的方式解释性的语言 （ACPI 源代码语言或 ASL） 和执行环境 （ACPI 虚拟机）。 ASL 用于 ACPI 命名空间中定义命名的对象和[Microsoft ASL compiler](microsoft-asl-compiler.md)用于生成 ACPI 机器语言 (AML) 字节代码，以传输到 DSDT 中的操作系统。 收件箱[Windows ACPI 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)，Acpi.sys，实现 ACPI 虚拟机，并将 AML 字节代码解释。 AML 对象只是可能会返回说明信息。 或者，AML 对象可能是执行计算或执行 I/O 操作的方法。 一个*控制方法*是使用操作系统的设备驱动程序来实现平台硬件上的 I/O 操作的可执行 AML 对象。 ASL 使用 OpRegions 来抽象化各种操作系统中可访问的地址空间。 控制方法为一系列的与 OpRegions 中声明的命名字段接收和执行 I/O 操作。

有关 OpRegions 详细信息，请参阅部分 5.5.2.4，"访问到操作区域"，在[ACPI 5.0 规范](https://www.uefi.org/specifications)。 有关 ASL 和控制方法的详细信息，请参阅部分 5.5，"ACPI Namespace"ACPI 5.0 规范中。

Windows 提供用于开发和调试 ASL 代码的支持。 ASL 编译器包含拆装器以便实现者从调试目标加载命名空间。 ASL 编译器然后可用于将命名空间重新应用于快速原型设计和测试的目标，而无需刷新系统固件。 此外，Windows 内核调试程序，结合 Acpi.sys 驱动程序，经检查 (CHK) 版本支持跟踪以及分析 AML 执行。 有关详细信息，请参阅[AMLI 调试器](https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction-to-the-amli-debugger)。

## <a name="windows-smm-security-mitigations-table-wsmt"></a>Windows SMM 安全缓解措施表 (WSMT)


Windows SMM 安全缓解措施表 (WSMT) 规范包含创建使用支持 Windows 基于虚拟化的安全性 (VBS) 的 Windows 操作系统中使用的高级配置和电源接口 (ACPI) 表的详细信息功能。

此信息适用于以下操作系统：

Windows Server 2016

Windows 10，版本 1607

有关详细信息，请参阅[Windows SMM 安全缓解措施表 (WMST) 规范](https://go.microsoft.com/fwlink/p/?LinkId=786943)。

