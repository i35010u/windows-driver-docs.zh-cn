---
title: 其他 ACPI 命名空间对象
description: 对于某些特定类别的设备，需要在命名空间中的这些设备下显示其他 ACPI 命名空间对象。
ms.assetid: 41EA8C3D-F2C9-4BA9-A839-FCB66F271E3C
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: f5621dd3ba0a2ed10a28fd9c21fca689590253de
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968044"
---
# <a name="other-acpi-namespace-objects"></a>其他 ACPI 命名空间对象

对于某些特定类别的设备，需要在命名空间中的这些设备下显示其他高级配置和电源接口（ACPI）命名空间对象。 本部分列出了基于 SoC 的平台所需的其他对象。

## <a name="processor-identification-objects"></a>处理器识别对象

处理器必须在 ACPI 命名空间中枚举。 与 \\ \_ 平台上的其他设备一样，使用 "Device" 语句在 SB 下声明处理器。 处理器设备必须包含以下对象：

- \_HID： ACPI0007
- \_UID：与 MADT 中的处理器条目相匹配的唯一编号。

## <a name="display-specific-objects"></a>特定于显示的对象

有关显示特定对象的详细信息，请参阅[ACPI 5.0 规范](https://uefi.org/specifications)的附录 B "视频扩展"。

### <a name="display-specific-object-requirements"></a>特定于显示的对象要求

| 方法 | 说明                                        | 要求                                                                      |
|--------|----------------------------------------------------|----------------------------------------------------------------------------------|
| \_造成  | 启用/禁用输出切换。                   | 如果系统支持显示器切换或 LCD 亮度级别，则是必需的。          |
| \_DOD  | 枚举附加到显示适配器的所有设备。 | 如果集成控制器支持输出切换，则为必需。                     |
| \_CD-ROM  | 获取 ROM 数据。                                      | 如果 ROM 映像以专有格式存储，则是必需的。                           |
| \_GPD  | 获取后设备。                                   | 如果 \_ 实现了 VPO，则为必需。                                                |
| \_SPD  | 设置后设备。                                   | 如果 \_ 实现了 VPO，则为必需。                                                |
| \_VPO  | 视频帖子选项。                                | 如果系统支持更改 VGA 后设备，则是必需的。                            |
| \_ADR  | 返回此设备的唯一 ID。              | 必需。                                                                        |
| \_BCL  | 支持的亮度控制级别的查询列表。 | 如果嵌入式 LCD 支持亮度控制，则是必需的。                            |
| \_BCM  | 设置亮度级别。                          | 如果 \_ 实现了 BCL，则为必需。                                                |
| \_DDC  | 返回此设备的 EDID。                   | 如果嵌入的 LCD 不支持通过标准接口返回 EDID，则是必需的。 |
| \_DC  | 返回输出设备的状态。                    | 如果系统支持显示切换（通过热键），则是必需的。                  |
| \_DG  | 查询图形状态。                              | 如果系统支持显示切换（通过热键），则是必需的。                  |
| \_DSS  | 设备状态集。                                  | 如果系统支持显示切换（通过热键），则是必需的。                  |

## <a name="usb-host-controllers-and-devices"></a>USB 主机控制器和设备

USB 主机控制器用于连接内部和外部设备的 SoC 平台。 Windows 包括符合 EHCI 或 XHCI 规范的标准 USB 主机控制器的收件箱驱动程序。

在基于 SoC 的平台上，可以通过 ACPI 枚举 USB 主机控制器。 当枚举和配置兼容的 USB 硬件时，Windows 使用以下 ACPI 命名空间对象：

- 供应商分配的符合 ACPI 的硬件 ID （ \_ HID）。

- 唯一 ID （ \_ UID）对象，如果命名空间中有多个 USB 控制器实例（即，具有相同设备标识对象的两个或多个节点）。

- \_适用于 EHCI 或 XHCI 标准兼容 USB 主机控制器（EHCI： PNP0D20）的兼容 ID （CID），（XHCI： PNP0D10）。

- 分配到 USB 控制器的当前资源设置（ \_ CRS）。 控制器的资源在适当的硬件接口规范（EHCI 或 XHCI）中进行了介绍。

### <a name="usb-device-specific-method-_dsm"></a>USB 设备特定方法（ \_ DSM）

Windows 定义了特定于设备的方法（ \_ DSM）来支持 USB 子系统的设备特定于设备的配置。 有关详细信息，请参阅[USB 特定于设备的方法](usb-device-specific-method---dsm-.md)。

### <a name="usb-integrated-transaction-translator-tt-support-_hrv"></a>USB 集成事务转换器（TT）支持（ \_ HRV）

标准 EHCI 主机控制器仅支持高速 USB 设备。 在 SoC 平台上，Windows 支持两个常见的与 EHCI 兼容的主机控制器的设计，它们实现了用于低速和全速 USB 设备的集成事务转换器。 硬件修订（ \_ HRV）对象指示 USB 主机控制器驱动程序的集成 TT 支持类型。

\_根据以下条件设置 HRV：

- **NoIntegratedTT- \_ HRV = 0**

    标准 EHCI 主机控制器不实现集成事务翻译，且 \_ HRV 值为0只对这些控制器有效。 不需要为 \_ 这些控制器包含 HRV 对象。

- **IntegratedTTSpeedInPortSc- \_ HRV = 1**

    启用集成 TT 支持。 此界面风格包含 PORTSC 注册本身中的 LowSpeed 和 HiSpeed 位。 这些位分别分别为位偏移26和27。 确定速度时，EHCI 驱动程序将读取 PORTSC，并从这些位提取速度信息。

- **IntegratedTTSpeedInHostPc- \_ HRV = 2**

    启用集成 TT 支持。 此界面风格包含单独 HOSTPC 寄存器中的 LowSpeed 和 HiSpeed 位。 当 EHCI 驱动程序需要确定端口速度时，它将读取对应于相关端口的 HOSTPC 寄存器，并提取速度信息。

### <a name="usb-xhci-d3cold-support"></a>USB XHCI D3cold 支持

除了选择性挂起外，连接到 XHCI 控制器的内部 USB 设备还可以进入 D3cold 状态，并在不使用时关闭电源。 有关详细信息，请参阅[设备电源管理](device-power-management.md)。 所有 USB 设备功能驱动程序都必须选择加入 D3cold。

### <a name="usb-port-specific-objects"></a>USB 端口专用对象

Windows 需要知道系统上 USB 端口的可见性和连接能力。 为了向用户提供有关端口和设备的准确信息，这是必需的。 将使用两个对象（物理设备位置（ \_ PLD）和 USB 端口功能（ \_ UPC））来实现此目的。 有关详细信息，请参阅以下主题：

- \_ \_ [ACPI 5.0 规范](https://uefi.org/specifications)中的6.1.6、"设备标识对象" 和 "9.13.1"、"USB 2.0 主机控制器和 UPC 和 PLD" 部分。

- [使用 ACPI 配置计算机上的 USB 端口](https://docs.microsoft.com/windows-hardware/drivers/install/using-acpi-to-configure-usb-ports-on-a-computer)。

## <a name="sd-host-controllers-and-devices"></a>SD 主机控制器和设备

SD 主机控制器用于 SoC 平台，可用于访问存储和 i/o 设备。 Windows 包括 SDA-standard 主机控制器硬件的收件箱驱动程序。 为了与此驱动程序兼容，SD 主机控制器设备必须符合 SD 关联的[Sd 主机控制器规范](https://www.sdcard.org/developers/overview/host_controller/)。

在 SoC 平台上，可通过 ACPI 枚举 SD 主机控制器。 枚举和配置兼容的 SD 硬件时，Windows 使用以下 ACPI 命名空间对象：

- 供应商分配的符合 ACPI 的硬件 ID （ \_ HID）。

- 唯一 ID （ \_ UID）对象，如果命名空间中有一个 SD 控制器实例（即，具有相同设备标识对象的两个或多个节点）。

- \_符合 SDA 标准的 SD 主机控制器（PNP0D40）的兼容 ID （CID）。

- 分配给控制器的当前资源设置（ \_ CRS）。 控制器的资源如下所述：

  - 包括所有已实现槽的硬件资源。 槽是用于内存或 i/o 设备的 SDIO 总线上的连接点。 每个槽都与一组标准寄存器和 SD 主机控制器中的中断相关联，该主机控制器用于与连接的设备进行通信。 SD 主机控制器可以实现任意数量的插槽，但在 SoC 平台上通常只有一个。

  - 槽资源一起列出，按槽号顺序排列（第0插槽的资源是第一个，槽1的资源是第二个，依此类推）。

  - 对于每个槽，按以下顺序列出资源：

    - 槽的 SD 标准寄存器集的基址。

    - 槽的 SD 标准中断。

    - 用于发送信号卡插入和删除的槽的 GPIO 中断资源（如果在所有电源状态中都不支持标准 SD 卡检测接口）。

    - 槽的 GPIO 输入资源，用于读取卡是否当前位于槽中（如果在所有电源状态中都不支持标准 SD 卡检测接口）。 使用与插入/删除中断相同的 pin。

    - 用于读取槽中的卡是否受写保护的另一个 GPIO 输入资源（如果在所有电源状态中都不支持标准 SD 写入保护接口）。

中断必须是支持唤醒的（描述为 "SharedAndWake" 或 "ExclusiveAndWake"）。

### <a name="embedded-sd-devices"></a>嵌入式 SD 设备

Sd 连接的设备由 SD bus 驱动程序枚举。 集成到平台中的 SD 设备还必须作为 SD 主机控制器的子项列在 ACPI 命名空间中。 此要求使操作系统能够将总线枚举设备与通过 ACPI 对象为设备提供的特定于平台的属性（例如，非 removability、设备电源状态、GPIO 或使用的 SPB 资源等）相关联。 若要建立此关联，设备命名空间需要 Address （ \_ ADR）对象，该对象会在 SDIO 总线上传达设备的地址。 \_ADR 对象返回整数。

对于 SDIO 总线，此整数的值定义如下：

- 高位字–槽号（0–第一个槽）

- Low word-函数编号（有关定义，请参阅 SD 规范。）

嵌入的 SD 设备命名空间还必须包括：

- 返回0的 Remove 方法（ \_ RMV）对象，指示无法删除设备。

- \_设备需要的 sideband 资源的 CRS 对象（如 GPIO 引脚或 SPB 连接）（如果需要）。

## <a name="imaging-class-devices-cameras"></a>成像类设备（照相机）

照相机设备可由图形驱动程序或 USB 来枚举。 在任一情况下，Windows 都需要知道照相机的物理位置，以便可以显示适当的 UI。 要执行此操作，请在 ACPI 命名空间中包含内置于系统机箱的相机设备，并将其固定方向包含在 ACPI 命名空间中，并提供物理设备位置（ \_ PLD）对象。 这需要：

- 照相机设备显示为枚举器设备（GPU 设备或 USB 设备）的子（嵌套设备）。

- 用于提供地址（ \_ ADR）对象的相机设备，该对象包含父设备总线上相机的地址。

  - 对于 USB，请参阅下一节中的 " **ACPI namespace 层次结构和 \_ ADR FOR embedded USB 设备**"。

  - 对于图形，这是在 \_ GPU 设备下提供的 DOD 方法中指定的标识符。 有关详细信息，请参阅 ACPI 5.0 规范的附录 B "视频扩展"。

- 照相机设备，用于提供 \_ PLD 对象。

- 如果照相机驱动程序所需的任何 sideband 资源（例如 GPIO 中断或 i/o 连接或 SPB 连接），则将 \_ 为这些资源提供 CRS 对象。

在 \_ PLD 对象中，将**面板**字段（bits 67-69）、**盖子**字段（位66）和**停靠**字段（bit 65）设置为装入照相机的图面的正确值。 所有其他字段是可选的。 对于手持式移动设备（包括平板电脑），前面板是一个包含显示屏幕的面板，其原点位于左下角，在纵向方向上查看。 使用此引用时，"前面" 表示相机查看用户（网络摄像机），而 "后退" 表示相机视图远离用户（仍为相机或视频摄像机）。 有关详细信息，请参阅 6.1.8 \_ 中[5.0](https://uefi.org/specifications)的 "PLD （设备的物理位置）" 部分。

### <a name="acpi-namespace-hierarchy-and-_adr-for-embedded-usb-devices"></a>用于嵌入式 USB 设备的 ACPI 命名空间层次结构和 \_ ADR

将嵌入式 USB 设备添加到 ACPI 命名空间时，设备节点的层次结构必须与 Windows USB 驱动程序所枚举的设备的层次结构完全匹配。 可以通过在其 "按连接查看" 模式下检查 Windows 设备管理器来确定这一点。 必须包含从 USB 主机控制器开始向下扩展到嵌入式设备的整个层次结构。 每个设备设备管理器中提供的 "Address" 属性是固件必须在设备的 ADR 中报告的地址 \_ 。

[ACPI 5.0 规范](https://uefi.org/specifications)定义了 USB 设备的地址，如下所示：

**USB 根集线器**：仅限主机控制器的子节点。 它 \_ 的 ADR 必须为0。 不允许使用任何其他子级或 \_ ADR 值。

**USB 端口**：端口号（1-n）


连接到特定端口的 USB 设备共享该端口的地址。

如果连接到端口的设备是复合 USB 设备，则复合设备中的函数必须使用以下地址：

**复合 usb 设备内的 USB 函数**：复合设备连接到的端口端口号，以及函数的第一个接口号。 （算术加法）。


有关详细信息，请参阅[标识内部照相机的位置](https://docs.microsoft.com/windows-hardware/drivers/devapps/identifying-the-location-of-internal-cameras)。

### <a name="asl-code-examples"></a>ASL 代码示例

以下 ASL 代码示例描述了直接连接到 USB 端口3的 USB 网络摄像机。

```asl
Device (EHCI) {
    ...  // Objects required for EHCI devices
    Device {RHUB) {         // the Root HUB
     Name (_ADR, ZERO)      // Address is always 0.
     Device (CAM0) {          // Camera connected directly to USB
                       //   port number 3 under the Root.
            Name (_ADR, 3)      // Address is the same as the port.
            Method (_PLD, 0, Serialized) {...}
            }  //  End of Camera device
    } // End of Root Hub Device
}  // End of EHCI device
```

下面的 ASL 代码示例介绍了将网络摄像头作为函数2实现的 USB 复合设备。

```asl
Device (EHCI) {
    ...  // Objects required for EHCI devices
    Device {RHUB) {
     Name (_ADR, ZERO)
     Device (CUSB) {        // Composite USB device
                    //   connected to USB port number 3
                    //   under the Root.
            Name (_ADR, 3)      // Address is the same as the port.
            Device (CAM0) { // Camera function within the
                    //   Composite USB device.
                Name (_ADR, 5)  // Camera function has a first
                    //   Interface number of 2, so
                    //   Address is 3 + 2  = 5.
                Method (_PLD, 0, Serialized) {...}
            }  //  End of Camera device
        } // End of Composite USB Device
    } // End of Root Hub Device
}  // End of EHCI device
```

以下 ASL 代码示例介绍了通过 I2C 连接的网络摄像机。

```asl
Device (GPU0) {
    ... // Other objects required for graphics devices
    Name (_DOD, Package ()  // Identifies the children of this graphics device.
                // Each integer must be unique within the GPU0 namespace.
                {
                    0x00024321,  // The ID for CAM0. It is a non-VGA
                    //   device, cannot be detected by
                    //   the VGA BIOS, and uses a vendor-
                    //   specific ID format in bits 15:0
                    //   (see the _DOD specification).
                    ...     // Other child device IDs (for
                    //   example, display output ports)
                })
    Device (CAM0) {
        Name (_ADR, 0x00024321) // The identifier for this device
                    //   (Same as in _DOD above)
        Name (_CRS, ResourceTemplate()
            {
            // I2C Resource
            // GPIO interrupt resource(s), if required by
            //   driver
            // GPIO I/O resource(s), if required by driver
                ...
            })
        Method (_PLD, 0, Serialized) {...}
    } // End of CAM0 device
} // End of GPU0 device
```

## <a name="hid-over-i2c-devices"></a>HID-over I2C 设备

Windows 包含用于人体学接口设备（HID）的类驱动程序。 此驱动程序支持对各种输入设备（如触控面板、键盘、鼠标和传感器）的通用支持。 在 SoC 平台上，HID 设备可以通过 I2C 连接到平台，并由 ACPI 枚举。 为了与 Windows 中的 HID 类支持兼容，使用了以下命名空间对象：

- 特定于供应商的 \_ HID

- \_PNP0C50 的 CID

- \_CRS：

  - 用于访问设备的 I2CSerialBusConnection 资源

  - 用于中断的 GpioInt 资源

- 用于在 \_ 设备中返回 HID 描述符注册地址的 HIDI2C DSM 方法。 有关详细信息，请参阅[HIDI2C 设备特定方法（ \_ DSM）](hidi2c-device-specific-method---dsm-.md)。

## <a name="button-devices"></a>按钮设备

对于 SoC 平台，Windows 支持 ACPI 定义的控制方法电源按钮，以及与 Windows 兼容的五按钮数组。 "电源" 按钮（无论是作为 ACPI 控制方法电源按钮还是作为 Windows 兼容的按钮数组的一部分实现的）执行以下操作：

- 使平台启动（如果它处于关闭状态）。

- 当按住时，生成电源按钮重写事件。 有关详细信息，请参阅 ACPI 5.0 规范的 "电源按钮替代" 部分。

### <a name="control-method-power-button"></a>Control 方法电源按钮

使用内置或连接键盘的 Clamshell 设计和其他系统，使用 GPIO-已发出 acpi 的 ACPI 事件（ACPI 5.0 规范的第5.6.5 部分）实现 ACPI 定义的控制方法电源按钮（ACPI 5.0 规范的部分4.8.2.2.1.2）。 若要支持电源按钮设备，命名空间为：

- 将电源按钮的 GPIO 中断 pin 描述为非共享（独占） GPIO 中断资源。

- 列出电源按钮在 \_ 其所连接的 gpio 控制器的 AEI 对象中的 GPIO 中断资源。

- 在 GPIO 控制器设备下提供关联的事件方法（Lxx/Exx/.EVT）。 此事件方法通知操作系统中发生按钮事件的控件方法按钮驱动程序。

有关详细信息，请参阅[适用于 Windows 8 平板电脑和可转换设备的硬件按钮](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613928(v=vs.85))。

### <a name="windows-compatible-button-array"></a>与 Windows 兼容的按钮数组

对于 touch （无键盘）平台（如清单），Windows 为包含五个按钮的数组提供通用驱动程序。 数组中的每个按钮都具有其定义的函数（请参阅下面列表中的编号项），并且某些 "按住" 按钮组合在 UI 中具有其他含义。 没有定义需要保持电源按钮的按钮组合。 为了与 Windows 收件箱按钮驱动程序兼容，实现了与 Windows 兼容的按钮阵列 ACPI 设备。 设备定义如下：

- 这五个按钮中的每一个都连接到其在平台上的专用中断 pin。

- 每个中断 pin 配置为在两个边缘（ActiveBoth）中断的非共享（独占）、边缘触发（边缘）中断资源。

- 设备命名空间包含供应商定义 \_ 的 HID 以及 \_ PNP0C40 的 CID。

- CRS 对象中的 GPIO 中断资源 \_ 按以下顺序列出：

    1. 对应于 "电源" 按钮的中断

        "电源" 按钮必须支持唤醒（ExclusiveAndWake）。

    1. 对应于 "Windows" 按钮的中断

        Windows 按钮必须是唤醒功能（ExclusiveAndWake）。

    1. 对应于 "音量增加" 按钮的中断

        "调高" 按钮不能是唤醒功能（必须使用独占）。

    1. 对应于 "向下移动" 按钮的中断

        "向下移动" 按钮不能支持唤醒功能（必须使用独占模式）。

    1. 对应于 "旋转锁定" 按钮的中断（如果支持）

        "旋转锁定" 按钮不得支持唤醒（必须使用独占）。

有关详细信息，请参阅[适用于 Windows 8 平板电脑和可转换设备的硬件按钮](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613928(v=vs.85))。

为了支持 Windows 按钮 UI 的演变，Windows 为 Windows 按钮阵列设备定义了设备特定的方法（ \_ DSM）。 有关详细信息，请参阅[Windows 按钮阵列特定于设备的方法（ \_ DSM）](windows-button-array-device-specific-method---dsm-.md)。

## <a name="dock-and-convertible-pc-sensing-devices"></a>停靠和可转换 PC 感知设备

Windows 通过使用 ACPI 命名空间中的两个感应设备支持改装（clamshell/tablet combos）。 Windows 收件箱按钮驱动程序支持这些设备。 请注意，适用于按钮阵列设备的相同要求也适用于这些设备：

- GPIO ActiveBoth 中断必须连接到已在 SoC 连接的 gpio 控制器上（而不是连接到 SPB 连接的 GPIO 控制器）。

- GPIO 控制器必须支持级别模式中断和动态极性 reprogramming。

- GPIO 控制器驱动程序必须使用[GPIO framework 扩展](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpioclx-i-o-and-interrupt-interfaces)（**GpioClx**）提供的 ActiveBoth 仿真。

- 如果断言状态（"已停靠" 或 "已转换"）的逻辑级别不为断言，则需要 GPIO 控制器 \_ DSM 方法来重写 gpio 驱动程序堆栈的默认行为。 有关详细信息，请参阅[常规用途 i/o （GPIO）](general-purpose-i-o--gpio-.md)主题中的**GPIO 控制器设备**部分。

有关详细信息，请参阅[适用于 Windows 8 平板电脑和可转换设备的硬件按钮](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613928(v=vs.85))。

### <a name="dock-sensing-device"></a>固定感应设备

当插接连接到系统或从系统中断开连接时，插接感应设备将中断系统。 此模式更改信息用于根据需要更新用户输入和输出体验。 设备的命名空间需要：

- 特定于供应商的 \_ HID

- \_PNP0C70 的 CID

- \_具有一个 ActiveBoth 中断的 CRS

    中断不能是唤醒功能。

### <a name="convertible-pc-sensing-device"></a>可转换的 PC 感应设备

当可转换的 PC 从平板电脑切换到 clamshell 外形规格时，可转换的电脑感应设备将中断系统。 此模式更改信息用于根据需要更新用户输入和输出体验。 设备的命名空间需要：

- 特定于供应商的 \_ HID

- \_PNP0C60 的 CID

- \_具有一个 ActiveBoth 中断的 CRS

    中断不能是唤醒功能。
