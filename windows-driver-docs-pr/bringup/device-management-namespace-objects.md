---
title: 设备管理命名空间对象
description: ACPI 5.0 规范定义了几种类型的命名空间对象的可用于管理设备。
ms.assetid: 26C3312D-B1B0-4843-BF4E-1B03630C0BDD
ms.date: 06/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: dc29478adbe553c1d9ab05456ebca8a6b0348eb5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364570"
---
# <a name="device-management-namespace-objects"></a>设备管理命名空间对象


[ACPI 5.0 规范](https://uefi.org/specifications)定义多种类型的命名空间可用于管理设备的对象。 例如，设备标识对象包含设备的连接到总线，例如 I2C，不支持子设备的硬件枚举的标识的信息。 其他类型的命名空间对象可以指定系统资源、 描述设备的依赖关系，并指示哪些设备可以被禁用。

## <a name="device-identification-in-windows"></a>在 Windows 中的设备标识


Windows 即插即用和播放查找并加载设备驱动程序基于提供的设备的枚举器的设备标识符。 枚举器是知道如何提取设备中的标识信息的总线驱动程序。 （如 PCI、 SD 和 USB） 某些总线具有硬件定义的机制来执行此提取。 对于执行不 （例如，处理器总线或简单的外围总线） 的总线，ACPI 命名空间中定义标识对象。

[Windows ACPI 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)，Acpi.sys，组装成各种不同的非常具体而言，可以识别设备的设备标识符字符串或非常一般情况下，具体取决于驱动程序需要这些对象中找到的值。 下面是一些要识别 ACPI 枚举设备所创建的字符串模式：

```syntax
ACPI\VEN_vvv[v]&DEV_dddd&SUBSYS_sss[s]nnnn&REV_rrrr
ACPI\VEN_vvv[v]&DEV_dddd&SUBSYS_sss[s]nnnn
ACPI\VEN_vvv[v]&DEV_dddd&REV_rrrr
ACPI\VEN_vvv[v]&DEV_dddd
ACPI\vvv[v]dddd
```

您所见 Windows 创建的设备标识符为你的设备通过设备管理器中打开并检查**硬件 Id**并**兼容 Id**枚举设备的属性。 每个这些字符串均可用于标识要为该设备加载的驱动程序的 INF 文件中进行指定。 INF 相匹配的顺序是从最具体的硬件标识符 （优先级最高驱动程序） 到最不具体的标识符 （优先级最低的驱动程序），以便了解更多有关设备的特定功能的驱动程序可以替换这些小于特定 （并因此支持的设备功能的一个子集）。

设备标识符应应用于 INF 匹配，并应永远不会分析或处理的设备驱动程序。 如果设备驱动程序都需要标识已加载以进行的特定硬件，推荐的方法是具有相应的注册表项在安装时的 INF 文件集。 驱动程序然后可以在初始化来获取所需的信息期间访问这些密钥。

## <a name="device-identification-in-acpi"></a>ACPI 中的设备标识


### <a name="hardware-id-hid"></a>硬件 ID (\_HID)

用于识别 ACPI 中的设备的最低要求是硬件 ID (\_HID) 对象。 \_HID 返回的格式的字符串"ABC\[D\]*xxxx*"，其中"ABC\[D\]"是一个 3 或 4 个字符字符串，标识 ("供应商 ID")，该设备的制造商和*xxxx*是一个标识特定设备制造的该供应商 ("设备 ID") 的十六进制数字。 行业供应商 Id 必须唯一。 Microsoft 会分配这些字符串以确保它们都是唯一。 可以从供应商 Id[插 ID-PNPID 请求](https://go.microsoft.com/fwlink/p/?linkid=330999)。

**请注意**  ACPI 5.0 还支持 PCI 分配供应商 Id 中使用\_HID 和其他标识对象，因此可能不需要从 Microsoft 获取供应商 ID。 有关硬件标识要求的详细信息，请参阅部分 6.1.5，"\_HID (硬件 ID)"的[ACPI 5.0 规范](https://uefi.org/specifications)。



### <a name="compatible-id-cid"></a>兼容 ID (\_CID)

Microsoft 已保留供与收件箱驱动程序随 Windows 兼容的设备供应商 ID"PNP"。 Windows 定义的具有此可用于加载设备提供 Windows 驱动程序的供应商 ID 使用的设备 Id 的数量。 单独的对象，兼容 ID (\_CID) 对象，用于返回这些标识符。 Windows 将始终首选硬件 Id (由\_HID) 通过兼容 Id (返回\_CID) INF 匹配和驱动程序所选内容中。 此首选项允许提供 Windows 驱动程序被视为默认驱动程序，如果供应商提供特定于设备的驱动程序不可用。 下表中的兼容 Id 新建用于 SoC 平台。

| 兼容 ID | 描述                                           |
|---------------|-------------------------------------------------------|
| PNP0C40       | Windows 兼容按钮数组                       |
| PNP0C50       | HID over I²C 兼容设备                         |
| PNP0C60       | 可转换便携式计算机显示传感器设备              |
| PNP0C70       | 停靠传感器设备                                    |
| PNP0D10       | 与标准调试 XHCI 符合 USB 控制器     |
| PNP0D15       | XHCI 符合 USB 控制器没有标准调试  |
| PNP0D20       | EHCI 符合 USB 控制器没有标准调试  |
| PNP0D25       | 与标准调试 EHCI 符合 USB 控制器     |
| PNP0D40       | SDA 符合标准的 SD 主控制器             |
| PNP0D80       | Windows 兼容系统电源管理控制器 |



### <a name="subsystem-id-sub-hardware-revision-hrv-and-class-cls"></a>子系统 ID (\_SUB)，硬件版本 (\_HRV)，和类 (\_CLS)

ACPI 5.0 定义\_SUB， \_HRV，并\_CLS 对象，可连同\_HID 创建更多唯一地标识特定的版本、 集成或使设备的硬件版本的标识符或若要指示中 PCI 定义设备类的成员身份。 这些对象通常是可选的但可能需要的 Windows 中的特定设备类。 有关这些对象的详细信息，请参阅部分 6.1，"设备标识对象"的[ACPI 5.0 规范](https://uefi.org/specifications)。

对于可维护性，则 Windows 硬件认证工具包 (HCK) 要求 OEM 系统上的设备 Id 为"由四部分组成的"Id。 四个部分是供应商 ID、 设备 ID、 子系统供应商 (OEM) ID 和子系统 (OEM) 设备 id。 因此，子系统 ID (\_子) 对象是所必需的 OEM 平台。

### <a name="device-specific-method-dsm"></a>特定于设备的方法 (\_DSM)

\_9.14.1，一节中定义 DSM 方法"\_DSM （设备特定的方法）"的[ACPI 5.0 规范](https://uefi.org/specifications)。 此方法提供单个、 特定于设备的数据和控制功能可以无冲突其他此类特定于设备的方法调用的设备驱动程序。 \_DSM 为特定设备或设备类定义保证不与其他 Uuid 冲突 UUID (GUID)。 对于每个 UUID，没有一组已定义的函数的\_DSM 方法可以实现以提供数据或执行的驱动程序控制功能。 特定于类的数据和数据格式中单独的特定于设备的类的规范提供了和中还讨论了[ACPI 特定于设备的方法](acpi-device-specific-methods.md)。

### <a name="address-adr-and-unique-id-uid"></a>地址 (\_ADR) 和唯一 ID (\_UID)

有三个其他要求的设备标识：

-   对于连接到硬件可枚举父总线 (例如，SDIO USB HSIC)，但具有特定于平台的功能或控件 （例如旁, 带电源或唤醒中断） 时，设备\_不使用 HID。 相反，设备标识符创建由父总线驱动程序 （如前面所述）。 在此情况下，不过，该地址对象 (\_ADR) 需要出现在 ACPI 名称空间的设备。 此对象使操作系统将总线枚举设备与 ACPI 描述功能或控件相关联。
-   在使用某一特定的 IP 块的多个实例位置，以便每个块具有相同设备标识的对象，唯一标识符的平台上 (\_UID) 对象，才可启用操作系统能够辨别不同的块。
-   在特定命名空间的范围中没有两个设备可以具有相同的名称。

## <a name="device-configuration-objects"></a>设备配置对象


用于标识命名空间中的每个设备，必须还被设备所使用的系统资源 （内存地址、 中断等） 报告由当前的资源设置 (\_CRS) 对象。 多个可能的资源配置的报告 (\_PR) 和更改设备的资源配置的控件 (\_SRS) 是受支持但为可选。

新 SoC 的平台是 GPIO 和设备使用的简单外围总线 （存储） 资源。 有关详细信息，请参阅[常规用途 I/O (GPIO)](general-purpose-i-o--gpio-.md)并[简单外围总线 （存储）](simple-peripheral-bus--spb-.md)。

此外新出现的 SoC 平台是一个常规用途的固定的 DMA 描述符。 FixedDMA 描述符支持由多个系统设备上共享 DMA 控制器硬件。 FixedDMA 描述符中列出了以静态方式分配给特定系统设备的 DMA 资源 （请求行和通道寄存器）。 有关详细信息，请参阅部分 19.5.49，"FixedDMA （DMA 资源描述符宏）"的[ACPI 5.0 规范](https://uefi.org/specifications)。

### <a name="device-status-changes"></a>设备状态变化

ACPI 枚举设备可以禁用或删除的原因有多种。 状态 (\_STA) 对象提供以启用此类状态会改变以传达给操作系统。 有关的说明\_STA，请参阅部分 6.3.7 [ACPI 5.0 规范](https://uefi.org/specifications)。 Windows 使用\_STA 来确定是否应设备枚举、 显示为已禁用，或对用户不可见。 在固件中的此控件可用于许多应用程序，包括停靠和 USB OTG 函数主机切换。

此外，ACPI 提供 ASL 可用于通知的事件在平台中，如要停靠的一部分删除设备驱动程序的通知机制。 一般情况下，当 ACPI 设备的状态更改，固件必须执行的"设备检查"总线检查"通知会导致 Windows 重新枚举设备并重新评估其\_sta。 有关 ACPI 通知的信息，请参阅 5.6.6，"设备对象通知"部分的[ACPI 5.0 规范](https://uefi.org/specifications)。

## <a name="enabledisable"></a>启用/禁用


作为 Windows 即插即用和播放的一部分，驱动程序必须能够动态启用和禁用用户或系统 （例如，对于更新驱动程序）。

在 SoC 设备集成到 SoC 芯片，并且不能删除。 适用于大多数上 SoC 设备驱动程序可以启用和禁用的要求也被如此。 对于这些驱动程序不受限制的没有用于指示该驱动程序支持有序地删除驱动程序接口。 有关详细信息，请参阅上标题为"减少即插即用要求的 SoC 驱动程序"的文档[Microsoft Connect 网站](https://aka.ms/connect-redirect?DownloadID=47560)。

如果驱动程序支持有序地删除，并且可以禁用设备硬件 （即，设备可以配置为停止访问其已分配的资源），则该设备的 ACPI 命名空间节点可以包括禁用 (\_显示) 对象。 此方法将由操作系统进行评估时删除该驱动程序。 使用\_DIS 具有以下附加要求：

-   \_只要设备已被禁用，STA 必须清除"启用和解码及其资源"位。
-   设备必须提供设置资源设置 (\_SRS) 对象来重新启用的设备硬件，并设置中上述位\_sta。

有关详细信息，请参阅部分 6.2.3 (\_显示)，6.2.15 (\_SRS)，和 6.3.7 (\_STA) 的[ACPI 5.0 规范](https://uefi.org/specifications)。

## <a name="device-dependencies"></a>设备依赖关系


通常情况下，在特定平台上的设备之间有硬件依赖项。 Windows 要求，以便它可以确保所有设备都正常操作更改为动态系统中描述了所有此类依赖项 (删除设备电源，驱动程序将停止并启动，等等)。 ACPI，在设备之间的依赖关系所述的以下方法：

1.  **Namespace 层次结构**。 是 （作为另一台设备的命名空间内的设备列出） 的子设备的任何设备是依赖于父设备。 例如，USB HSIC 设备是依赖于端口 （父） 和连接到控制器 （祖父）。 同样，列出在系统内存管理单元 (MMU) 设备的命名空间中的 GPU 设备是依赖于 MMU 设备。
2.  **资源连接**。 设备连接到 GPIO 或存储控制器都依赖于这些控制器。 在设备的连接资源的包含描述这种类型的依赖关系\_CRS。
3.  **OpRegion 依赖项**。 对于使用 OpRegions 执行 I/O 的 ASL 控制方法，依赖项是隐式未知操作系统因为它们只在控制方法计算确定。 此问题是特别适用于 GeneralPurposeIO 和 GenericSerialBus OpRegions 插驱动程序在其中提供到区域的访问权限。 若要缓解此问题，ACPI 定义 OpRegion 依赖关系 (\_DEP) 对象。 \_应在任何设备命名空间，在其中 OpRegion （硬件资源） 引用的一种控制方法，并 1 和 2 以上都不已应用中使用 DEP，引用的 OpRegion 连接资源。 有关详细信息，请参阅部分 6.5.8，"\_DEP （操作区域依赖项）"的[ACPI 5.0 规范](https://uefi.org/specifications)。

有也可以是软件依赖项之间的设备驱动程序。 此外必须描述这些依赖关系。 有关详情，请参阅以下资源：

-   有关驱动程序加载顺序的依赖项，请参阅[指定驱动程序加载顺序](https://docs.microsoft.com/windows-hardware/drivers/install/specifying-driver-load-order)。
-   有关电源关系依赖项，请参阅：

    -   [**IoInvalidateDeviceRelations** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinvalidatedevicerelations)例程 (若要触发建立 power 关系，请调用**IoInvalidateDeviceRelations**例程替换**设备\_关系\_键入**枚举值**PowerRelations**。)
    -   [**IRP\_MN\_查询\_设备\_关系**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)
    -   [枚举的总线上的设备](https://docs.microsoft.com/windows-hardware/drivers/wdf/enumerating-the-devices-on-a-bus)
    -   [动态枚举](https://docs.microsoft.com/windows-hardware/drivers/wdf/dynamic-enumeration)
    -   [**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks) method








