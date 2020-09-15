---
title: 设备管理命名空间对象
description: ACPI 5.0 规范定义了几种可用于管理设备的命名空间对象类型。
ms.assetid: 26C3312D-B1B0-4843-BF4E-1B03630C0BDD
ms.date: 06/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: b999109038eb59a54b91a2438fe96da832c19f28
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101534"
---
# <a name="device-management-namespace-objects"></a>设备管理命名空间对象

[ACPI 5.0 规范](https://uefi.org/specifications)定义了几种可用于管理设备的命名空间对象类型。 例如，设备标识对象包含连接到总线的设备的标识信息，例如 I2C，不支持子设备的硬件枚举。 其他类型的命名空间对象可以指定系统资源、描述设备依赖关系，并指明哪些设备可以禁用。

## <a name="device-identification-in-windows"></a>Windows 中的设备标识

Windows 即插即用根据设备枚举器提供的设备标识符，查找和加载设备驱动程序。 枚举器是知道如何从设备提取标识信息的总线驱动程序。 某些总线 (如 PCI、SD 和 USB) 具有硬件定义机制来执行此提取。 对于不 (例如处理器总线或简单外围总线) 的总线，ACPI 在命名空间中定义标识对象。

[WINDOWS ACPI 驱动程序](../kernel/acpi-driver.md)Acpi.sys 将这些对象中的值汇编成各种设备标识符字符串，这些字符串可以根据驱动程序的需要，非常明确地识别设备，也可以是非常普遍的。 为了识别 ACPI 枚举设备而创建的某些字符串模式为：

```syntax
ACPI\VEN_vvv[v]&DEV_dddd&SUBSYS_sss[s]nnnn&REV_rrrr
ACPI\VEN_vvv[v]&DEV_dddd&SUBSYS_sss[s]nnnn
ACPI\VEN_vvv[v]&DEV_dddd&REV_rrrr
ACPI\VEN_vvv[v]&DEV_dddd
ACPI\vvv[v]dddd
```

你可以通过打开设备管理器并检查枚举设备的 **硬件 id** 和 **兼容 id** 属性，来查看 Windows 为你的设备创建的设备标识符。 可以在 INF 文件中指定每个字符串，以确定要为设备加载的驱动程序。 INF 匹配的顺序是从最具体的硬件标识符 (最可取的驱动程序) 到最不特定的标识符， (最低优先级的驱动程序) ，因此，知道设备的特定功能的详细信息可以替换不太具体的 (的驱动程序，从而仅支持设备功能的一个子集。

设备标识符应仅用于 INF 匹配，不应由设备驱动程序进行分析或处理。 如果设备驱动程序需要标识其所加载的特定硬件，推荐的方法是在安装时让 INF 文件设置相应的注册表项。 然后，驱动程序可以在初始化过程中访问这些密钥以获取所需的信息。

## <a name="device-identification-in-acpi"></a>ACPI 中的设备标识

### <a name="hardware-id-_hid"></a> (HID) 的硬件 ID \_

在 ACPI 中标识设备的最低要求是 (\_ HID) 对象的硬件 ID。 \_HID 返回格式为 "ABC \[ d \] *xxxx*" 的字符串，其中 "abc \[ d \] " 是一个由三个或四个字符组成的字符串，用于标识设备制造商 ("供应商 id" ) ， *xxxx*是一个十六进制数字，用于标识由该供应商生产的特定设备 ("设备 ID" ) 。 供应商 Id 在整个行业中必须是唯一的。 Microsoft 会分配这些字符串以确保它们是唯一的。 可以从 [即插即用 ID-PNPID 请求](../install/plug-and-play-id---pnpid-request.md)中获取供应商 id。

> [!NOTE]
> ACPI 5.0 还支持在 HID 和其他标识对象中使用 PCI 分配的供应商 Id \_ ，因此你可能不需要从 Microsoft 获取供应商 id。 有关硬件标识要求的详细信息，请参阅 \_ [ACPI 5.0 规范](https://uefi.org/specifications)的 "HID (硬件 ID) " 部分。

### <a name="compatible-id-_cid"></a>CID) 兼容 ID (\_

对于与 Windows 附带的收件箱驱动程序兼容的设备，Microsoft 保留了供应商 ID "PNP"。 Windows 定义了多个与此供应商 ID 结合使用的设备 Id，该 ID 可用于为设备加载 Windows 提供的驱动程序。 一个单独的对象， (\_ CID) 对象的兼容 ID，用于返回这些标识符。 Windows 始终首选硬件 Id (由 \_ HID) 通过兼容 id 返回， (由 \_ CID) 在 INF 匹配和驱动程序选择中返回。 如果供应商提供的特定于设备的驱动程序不可用，则此首选项允许将 Windows 提供的驱动程序视为默认驱动程序。 下表中的兼容 Id 是新创建的，用于 SoC 平台。

| 兼容 ID | 说明 |
| --- | --- |
| PNP0C40  | 与 Windows 兼容的按钮数组 |
| PNP0C50  | HID-基于 I i2c 的设备 |
| PNP0C60  | 可转换笔记本电脑显示传感器设备 |
| PNP0C70  | 停靠传感器设备  |
| PNP0D10  | 标准调试的 XHCI 兼容 USB 控制器 |
| PNP0D15  | 不带标准调试的 XHCI 兼容 USB 控制器 |
| PNP0D20  | 不带标准调试的 EHCI 兼容 USB 控制器 |
| PNP0D25  | 标准调试的 EHCI 兼容 USB 控制器 |
| PNP0D40  | SDA 标准相容 SD 主机控制器 |
| PNP0D80  | 与 Windows 兼容的系统电源管理控制器 |

### <a name="subsystem-id-_sub-hardware-revision-_hrv-and-class-_cls"></a>子系统 ID (\_ SUB) ，硬件修订 (\_ HRV) ，类 (\_ CLS) 

ACPI 5.0 定义了 \_ SUB、 \_ HRV 和 \_ CLS 对象，这些对象可与 HID 一起使用， \_ 以创建更多地唯一标识设备的特定版本、集成或硬件修订版的标识符，或指示 PCI 定义的设备类中的成员身份。 这些对象通常是可选的，但可能是 Windows 中某些设备类所必需的。 有关这些对象的详细信息，请参阅 [ACPI 5.0 规范](https://uefi.org/specifications)的 "设备识别对象" 6.1 一节。

为实现可维护性，有一个 Windows 硬件认证工具包 (HCK) 要求 OEM 系统上的设备 Id 是 "四部分" Id。 这四个部分分别为供应商 ID、设备 ID、子系统供应商 (OEM) ID 和子系统 (OEM) 设备 ID。 因此， \_ 对于 OEM 平台，需要子系统 ID (SUB) 对象。

### <a name="device-specific-method-_dsm"></a> (DSM) 特定于设备的方法 \_

在 \_ \_ [ACPI 5.0 规范](https://uefi.org/specifications)的 "Dsm (设备特定方法) " 部分中定义 DSM 方法。 此方法提供了特定于设备的数据和控制函数，可由设备驱动程序调用，而不会与其他此类特定于设备的方法发生冲突。 \_特定设备或设备类的 DSM 定义一个 UUID (GUID) ，保证其不会与其他 uuid 冲突。 对于每个 UUID，可通过 DSM 方法实现一组定义的函数 \_ 来提供数据或为驱动程序执行控制功能。 类特定的数据和数据格式以单独的设备类规范提供，还在 [ACPI 设备特定的方法](acpi-device-specific-methods.md)中进行了介绍。

### <a name="address-_adr-and-unique-id-_uid"></a>Address (\_ ADR) 和 UNIQUE ID (\_ UID) 

设备标识有三个附加要求：

- 对于连接到硬件可枚举父总线的设备 (例如，SDIO、USB HSIC) ，但具有特定于平台的功能或控件 (例如，sideband 电源或唤醒中断) ， \_ 不使用该 HID。 相反，设备标识符由父总线驱动程序创建 (如之前) 所述。 但在这种情况下，ADR) 的 Address (对象必须 \_ 位于设备的 ACPI 命名空间中。 此对象使操作系统能够将总线枚举设备与 ACPI 描述的功能或控件相关联。
- 在使用特定 IP 块的多个实例的平台上，因此每个块都具有相同的设备标识对象，唯一标识符 (\_ UID) 对象，使操作系统能够区分块。
- 特定命名空间范围中的两个设备不能具有相同的名称。

## <a name="device-configuration-objects"></a>设备配置对象

对于命名空间中标识的每个设备，由设备使用的系统资源 (内存地址、中断等) 也必须由 CRS) 对象的当前资源 (设置报告 \_ 。  (pr) 的多个可能的资源配置 \_ 和用于更改设备资源配置 (SRS) 支持的控件的报告， \_ 但这是可选的。

用于 SoC 平台的新的是 GPIO 和简单的外围总线 (设备可使用的) 资源。 有关详细信息，请参阅 [常规用途 i/o (GPIO) ](general-purpose-i-o--gpio-.md) 和 [简单外围总线 (SPB) ](simple-peripheral-bus--spb-.md)。

另外，对于 SoC 平台，还可以使用常规用途固定 DMA 描述符。 FixedDMA 描述符支持多个系统设备共享 DMA 控制器硬件。 FixedDMA 描述符中列出了 DMA 资源 (请求线路和通道寄存器) 静态分配给特定的系统设备。 有关详细信息，请参阅 [ACPI 5.0 规范](https://uefi.org/specifications)的 "FIXEDDMA (DMA 资源描述符宏) " 部分。

### <a name="device-status-changes"></a>设备状态更改

出于多种原因，可以禁用或删除 ACPI 枚举设备。 \_提供 (STA) 对象的状态，以便将此类状态更改传递到操作系统。 有关 STA 的说明 \_ ，请参阅 [ACPI 5.0 规范](https://uefi.org/specifications)的6.3.7 部分。 Windows 使用 \_ STA 来确定是否应枚举设备、显示为已禁用或对用户不可见。 此控制在固件中适用于许多应用程序，包括停靠和 USB OTG 主机到功能切换。

此外，ACPI 还提供了一种通知机制，ASL 可以使用该机制来通知平台中事件的驱动程序，如作为插接的一部分被删除的设备。 通常，当 ACPI 设备的状态发生更改时，固件必须执行 "设备检查" 或 "总线检查" 通知，以使 Windows 重新枚举设备并重新评估其 \_ STA。 有关 ACPI 通知的信息，请参阅 [acpi 5.0 规范](https://uefi.org/specifications)的 "设备对象通知" 部分5.6.6。

## <a name="enabledisable"></a>启用/禁用

作为 Windows 即插即用的一部分，驱动程序必须能够由用户或系统 (动态启用和禁用，例如，) 更新驱动程序。

SoC 设备集成到 SoC 芯片，无法删除。 可从启用和禁用的要求中免除大多数 on SoC 设备的驱动程序。 对于那些不例外的驱动程序，有一些驱动程序接口用于指示驱动程序支持有序删除。 有关详细信息，请参阅 [Microsoft Connect 网站](/collaborate/connect-redirect?DownloadID=47560)上标题为 "降低 SoC 驱动程序的 PNP 要求" 的文档。

如果驱动程序支持序删除，并且可禁用设备硬件 (也就是说，可以将设备配置为停止访问其已分配资源) ，然后设备的 "ACPI 命名空间" 节点可以包括 "禁用 (" \_ ) 对象。 只要删除驱动程序，操作系统就会对此方法进行评估。 使用 \_ 拆装具有以下附加要求：

- \_如果设备被禁用，STA 必须清除 "已启用并解码其资源"。
- 设备必须提供 "设置资源设置" (\_ SRS) 对象，才能重新启用设备硬件并在 STA 中设置上述位 \_ 。

有关详细信息，请参阅 \_ ACPI 5.0 规范的 6.2.3 (拆装) 、6.2.15 (\_ SRS) 和 6.3.7 (\_ STA [ACPI 5.0 specification](https://uefi.org/specifications)) 部分。

## <a name="device-dependencies"></a>设备依赖关系

通常，特定平台上的设备之间存在硬件依赖关系。 Windows 要求描述所有此类依赖项，以便可以确保所有设备在系统中动态变化时正常运行 (设备电源已断开，驱动程序将停止并启动，等等) 。 在 ACPI 中，设备间的依赖关系按以下方式描述：

1. **命名空间层次结构**。 作为子设备的任何设备 (作为另一设备的命名空间中的设备列出) 依赖于父设备。 例如，USB HSIC 设备依赖于端口 (父) 和控制器 () 祖父连接到的控制器。 同样，系统内存管理单元的命名空间中列出的 GPU 设备 (MMU) 设备依赖于 MMU 设备。

1. **资源连接**。 连接到 GPIO 或 SPB 控制器的设备依赖于这些控制器。 这种类型的依赖关系是通过在设备 CRS 中包含连接资源来描述的 \_ 。

1. **OpRegion 依赖项**。 对于使用 OpRegions 执行 i/o 的 ASL 控制方法，操作系统不会隐式识别依赖项，因为它们仅在控件方法计算期间确定。 此问题特别适用于 GeneralPurposeIO 和 GenericSerialBus OpRegions，其中即插即用驱动程序提供对区域的访问权限。 为了缓解此问题，ACPI (DEP) 对象中定义了 OpRegion 依赖关系 \_ 。 \_DEP 应该在任何设备命名空间中使用，在该命名空间中，OpRegion (HW 资源) 由控制方法引用，上面的1个和第2项都不应用于引用的 OpRegion 的连接资源。 有关详细信息，请参阅 \_ [ACPI 5.0 规范](https://uefi.org/specifications)的 "DEP (操作区域依赖关系) " 部分。

设备驱动程序之间也可能存在软件依赖关系。 还必须描述这些依赖关系。

有关详细信息，请参阅以下资源：

- 对于驱动程序加载顺序依赖关系，请参阅 [指定驱动程序加载顺序](../install/specifying-driver-load-order.md)。

- 有关电源关系的依赖项，请参阅：

  - [IoInvalidateDeviceRelations](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations) (若要触发建立电源关系，请调用**设备 \_ 关系 \_ 类型**为 enum 值为**PowerRelations**的**IoInvalidateDeviceRelations**例程。 ) 
  
  - [IRP \_ MN \_ 查询 \_ 设备 \_ 关系](../kernel/irp-mn-query-device-relations.md)

  - [WdfDeviceInitSetPnpPowerEventCallbacks](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)

  - [枚举总线上的设备](../wdf/enumerating-the-devices-on-a-bus.md)

  - [动态枚举](../wdf/dynamic-enumeration.md)