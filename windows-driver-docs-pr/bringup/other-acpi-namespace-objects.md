---
title: 其他 ACPI 命名空间对象
description: 对于设备的某些特定的类，有其他的 ACPI 命名空间对象，以显示下命名空间中的这些设备的要求。
ms.assetid: 41EA8C3D-F2C9-4BA9-A839-FCB66F271E3C
ms.date: 05/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1c713953375df3baa245161244141325ac59261c
ms.sourcegitcommit: 3cdabbe0af52459e484e093a9e11da8f5312daf6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/26/2019
ms.locfileid: "58441933"
---
# <a name="other-acpi-namespace-objects"></a>其他 ACPI 命名空间对象

对于设备的某些特定的类，有其他高级配置和电源接口 (ACPI) 命名空间对象下方的命名空间中的这些设备出现的要求。 本部分列出了用于基于 SoC 的平台所需的其他对象。

## <a name="processor-identification-objects"></a>处理器标识对象

必须在 ACPI 名称空间中枚举的处理器。 下声明处理器\\ \_SB"设备"语句中，使用与在平台上的其他设备一样。 处理器的设备必须包含以下对象：

- \_HID:ACPI0007
- \_UID:匹配 MADT 中处理器的条目的唯一编号。

## <a name="display-specific-objects"></a>显示特定对象

显示特定对象的详细信息，请参阅附录 B，"视频 Extensions"的[ACPI 5.0 规范](https://www.uefi.org/specifications)。

### <a name="display-specific-object-requirements"></a>显示特定对象的要求

| 方法 | 描述                                        | 要求                                                                      |
|--------|----------------------------------------------------|----------------------------------------------------------------------------------|
| \_DOS  | 启用/禁用输出切换。                   | 所需的系统是否支持显示切换或 LCD 亮度级别。          |
| \_DOD  | 枚举连接以显示适配器的所有设备。 | 需要集成的控制器是否支持输出切换。                     |
| \_ROM  | 获取 ROM 数据。                                      | 所需如果 ROM 映像存储在专用格式。                           |
| \_GPD  | 获取 POST 设备。                                   | 如果使用\_VPO 实现。                                                |
| \_SPD  | 开机自检设备设置。                                   | 如果使用\_VPO 实现。                                                |
| \_VPO  | 视频 POST 选项。                                | 所需的系统是否支持不断变化的 post VGA 设备。                            |
| \_ADR  | 返回此设备的唯一 ID。              | 必需。                                                                        |
| \_BCL  | 支持的亮度控制级别的查询列表。 | 所需嵌入的 LCD 是否支持的亮度控制。                            |
| \_BCM  | 设置的亮度级别。                          | 如果使用\_BCL 实现。                                                |
| \_DDC  | 返回为此设备 EDID。                   | 所需嵌入的 LCD 不支持 EDID 返回通过标准接口。 |
| \_DCS  | 返回的输出设备的状态。                    | 所需的系统是否支持显示切换 （通过热键）。                  |
| \_DGS  | 查询图形状态。                              | 所需的系统是否支持显示切换 （通过热键）。                  |
| \_DSS  | 设备状态集。                                  | 所需的系统是否支持显示切换 （通过热键）。                  |

## <a name="usb-host-controllers-and-devices"></a>USB 主控制器和设备

USB 主控制器在 SoC 平台上可用来连接内部和外部设备。 Windows 包含符合 EHCI 或 XHCI 规范的标准 USB 主控制器的收件箱驱动程序。

SoC 基于在平台上，可由 ACPI 枚举 USB 主控制器。 Windows 使用以下 ACPI 命名空间对象枚举和配置兼容的 USB 硬件时：

- 供应商指派 ACPI 兼容的硬件 ID (\_HID)。
- 唯一 ID (\_UID) 对象，如果多个实例中的命名空间 （即，两个或多个节点具有相同的设备标识对象） 的 USB 控制器。
- 兼容 ID (\_CID) EHCI 或 XHCI 符合标准 USB 主控制器 (EHCI:PNP0D20)，(XHCI:PNP0D10)。
- 当前资源设置 (\_CRS) 分配给 USB 控制器。 控制器的资源进行了适当的硬件接口规范 （EHCI 或 XHCI） 中描述。

### <a name="usb-device-specific-method-dsm"></a>USB 设备特定的方法 (\_DSM)

Windows 定义的特定于设备的方法 (\_DSM) 以支持 USB 子系统的特定于设备的类的配置。 有关详细信息，请参阅[USB 设备特定的方法](usb-device-specific-method---dsm-.md)。

### <a name="usb-integrated-transaction-translator-tt-support-hrv"></a>USB 集成事务转换器 (TT) 支持 (\_HRV)

标准 EHCI 主控制器仅支持高速 USB 设备。 SoC 在平台上，Windows 支持两种常见设计的 EHCI 符合主机控制器实现低速和全速 USB 设备集成的事务处理翻译。 硬件版本 (\_HRV) 对象指示集成 TT 支持添加到 USB 主控制器驱动程序的类型。

\_HRV 设置根据以下条件：

- **NoIntegratedTT - \_HRV = 0**

    标准 EHCI 主控制器不会实现集成的事务处理翻译人员和\_HRV 值为 0 时才有效这些控制器。 不需要包括\_HRV 这些控制器对象。

- **IntegratedTTSpeedInPortSc - \_HRV = 1**

    启用集成的 TT 支持。 此风格的接口包括降低速度和中 PORTSC HiSpeed 位注册自身。 这些位分别位于 26 和 27、 的位偏移量。 在确定速度，EHCI 驱动程序将读取 PORTSC，并从这些位中提取的速度信息。

- **IntegratedTTSpeedInHostPc - \_HRV = 2**

    启用集成的 TT 支持。 此风格的接口包括在单独的 HOSTPC 寄存器降低速度和 HiSpeed 位。 当 EHCI 驱动程序需要确定端口速度时，它将读取对应于所需的端口的 HOSTPC 寄存器和提取的速度信息。

### <a name="usb-xhci-d3cold-support"></a>USB XHCI D3cold 支持

除了选择性挂起，可以将放入 D3cold 状态并关闭时不使用内部的 USB 设备连接到 XHCI 控制器。 有关详细信息，请参阅[设备电源管理](device-power-management.md)。 所有 USB 设备功能的驱动程序必须参加 D3cold 到。

### <a name="usb-port-specific-objects"></a>USB 端口特定的对象

Windows 需要知道的可见性和连接的功能的 USB 端口的系统上。 这是为了向有关端口和设备用户提供准确信息所必需的。 两个对象，物理设备的位置 (\_以前) 和 USB 端口功能 (\_UPC)，用于此目的。 有关详细信息，请参阅以下文章：

- 节 6.1.6、"设备标识对象"和 9.13.1，"USB 2.0 端口的主控制器和\_UPC 和\_以前"，在[ACPI 5.0 规范](https://www.uefi.org/specifications)。
- [使用 ACPI 的计算机上配置 USB 端口](https://docs.microsoft.com/windows-hardware/drivers/install/using-acpi-to-configure-usb-ports-on-a-computer)。

## <a name="sd-host-controllers-and-devices"></a>SD 主控制器和设备

SD 主机控制器使用 SoC 平台上进行存储，以及输入/输出设备的访问。 Windows 包括 SDA 标准主机控制器硬件的收件箱驱动程序。 使用此驱动程序的兼容性，SD 主机控制器设备必须符合 SD 关联[SD 主机控制器规范](https://www.sdcard.org/developers/overview/host_controller/)。

SoC 在平台上，可由 ACPI 枚举 SD 主控制器。 Windows 使用以下 ACPI 命名空间对象枚举和配置兼容 SD 硬件时：

- 供应商指派 ACPI 兼容的硬件 ID (\_HID)。
- 唯一 ID (\_UID) 对象，如果多个实例中的命名空间 （即，两个或多个节点具有相同的设备标识对象） 的 SD 控制器。
- 兼容 ID (\_CID) SDA 符合标准的 SD 主控制器 (PNP0D40)。
- 当前资源设置 (\_CRS) 分配给的控制器。 控制器的资源进行了描述，如下所示：

  - 中包含的所有实现的插槽的硬件资源。 在槽是内存或 I/O 设备 SDIO 总线上的连接点。 每个插槽都与一组标准的寄存器和 SD 主机控制器中的中断与已连接的设备一起使用的通信相关联。 SD 主机控制器可以实现任意数量的槽，但在 SoC 平台上没有通常只有一个。
  - 中的槽编号顺序在一起，列出槽资源 （槽 0 的资源是第一，在槽 1 的资源是第二个，依此类推）。
  - 为每个槽中，按以下顺序列出了资源：

        -   标准 SD 的基址的槽的集进行注册。
        -   在槽 SD 标准中断。
        -   GPIO 中断信号性沉寂卡插入和删除 （如果标准 SD 卡检测期间所有的电源状态，不支持接口） 的槽的资源。
        -   GPIO 输入读取的槽的资源是否卡位于当前槽中 （如果标准 SD 卡检测期间所有的电源状态，不支持接口）。 使用相同的 pin 作为插入/删除中断。
        -   第二个 GPIO 输入读取的资源是否在槽中的卡是写保护状态 （如果标准 SD 写保护接口不支持在所有的电源状态期间）。

必须支持唤醒的中断 （描述为"SharedAndWake"或"ExclusiveAndWake"）。

### <a name="embedded-sd-devices"></a>Embedded 的 SD 设备

SD 总线驱动程序通过枚举 SD 连接的设备。 集成到平台的 SD 设备还必须在 ACPI 名称空间作为 SD 主控制器的子级列出。 此要求使操作系统能够总线枚举设备相关联 ACPI 对象 （例如，非其可移除性、 设备的电源状态、 消耗的 GPIO 或存储资源等） 提供的设备的特定于平台的属性。 若要建立此关联，设备命名空间需要地址 (\_ADR) 对象，该通信 SDIO 总线上设备的地址对象。 \_ADR 对象返回一个整数。 对于 SDIO 总线中，此整数的值定义，如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td>SDIO 总线</td>
<td><p>高位字 – 槽编号 （0 – 第一个槽）</p>
<p>低位字 – 函数号 （请参阅 SD 定义的规范）。</p></td>
</tr>
</tbody>
</table>

此外必须包括嵌入的 SD 设备命名空间：

- 删除方法 (\_RMV)，则返回 0 （以指示不能删除该设备） 的对象。
- 一个\_CRS 设备要求 （如 GPIO 插针或存储的连接），如有必要的旁带资源的对象。

## <a name="imaging-class-devices-cameras"></a>图像处理类设备 （照相机）

通过图形驱动程序或通过 USB 可能枚举摄像机设备。 在任一情况下，Windows 需要知道的相机的物理位置，以便可以显示适当的用户界面。 若要执行此操作，内置的系统底盘和机械地修复方向的照相机设备 ACPI 名称空间中包含并提供物理设备位置 (\_以前) 对象。 这需要：

- 要显示为子级 （嵌套设备） 的枚举器设备 （GPU 设备或 USB 设备） 的摄像机设备。
- 摄像机设备提供的地址 (\_ADR) 对象，其中包含父设备的总线上的照相机的地址。

  - 有关 USB，请参阅**ACPI 命名空间层次结构和\_适用于 embedded USB 设备 ADR**中下一节。
  - 对于图形，这是中指定的标识符\_DOD 方法提供 GPU 设备下。 有关详细信息，请参阅附录 B，视频的"扩展"，ACPI 5.0 规范。

- 该摄像机设备提供\_以前对象。
- 如果有摄像机驱动程序 （如 GPIO 中断或 I/O 的连接或存储连接），需要任何旁带资源\_CRS 对象提供对这些资源。

在中\_以前对象**面板**字段 （位 67 69），**合上盖子**字段 （位 66） 和**停靠**字段 （位 65） 设置为正确值的图面装载照相机。 所有其他字段是可选的。 对于手持移动设备，包括平板电脑前, 面板是一个持有显示屏幕和其原点位于左下角显示查看纵向方向时。 使用此引用，"前"指示照相机视图用户 （网络摄像机），而"上一步"表示照相机视图即可从用户 （仍或视频摄像机）。 有关详细信息，请参阅，部分 6.1.8，"\_以前 （物理位置的设备）"，在[ACPI 5.0 规范](https://www.uefi.org/specifications)。

### <a name="acpi-namespace-hierarchy-and-adr-for-embedded-usb-devices"></a>ACPI 命名空间层次结构和\_ADR embedded USB 设备

将嵌入的 USB 设备添加到 ACPI 名称空间，当设备节点的层次结构必须完全匹配的 Windows USB 驱动程序通过枚举的设备。 这可以通过在"视图的连接"模式下查看 Windows 设备管理器来确定。 必须包含整个层次结构，从 USB 主控制器开始并扩展到嵌入式设备。 为每个设备固件必须报告的设备中的地址提供设备管理器中的"地址"属性\_ADR。

[ACPI 5.0 规范](https://www.uefi.org/specifications)定义 USB 设备的地址，如下所示：

|              |                                                                                                                  |
|--------------|------------------------------------------------------------------------------------------------------------------|
| USB 根集线器 | 主控制器仅子项。 它必须具有\_ADR 为 0。 没有其他子项或值的\_允许 ADR。 |
| USB 端口    | 端口号 (1-n)                                                                                                |

USB 设备连接到特定端口共享该端口的地址。

如果设备连接到的端口是复合的 USB 设备，复合设备中的函数必须使用以下地址：

|     |     |
| --- | --- |
| 在复合 USB 设备中的 USB 函数 | 复合设备连接到，加上函数的第一个接口号的端口的端口号。 （算术加法）。 |

有关详细信息，请参阅[确定内部相机位置的](https://go.microsoft.com/fwlink/p/?linkid=331060)。

### <a name="asl-code-examples"></a>ASL 代码示例

下面的 ASL 代码示例介绍直接连接到 USB 端口 3 USB 网络摄像机。

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

下面的 ASL 代码示例介绍实现为函数 2 网络摄像头的 USB 复合设备。

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

下面的 ASL 代码示例介绍了通过 I2C 连接的摄像头。

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

## <a name="hid-over-i2c-devices"></a>HID over I2C 设备

Windows 包括类驱动程序的人机接口设备 (HID)。 此驱动程序，输入设备 （如触摸面板、 键盘、 鼠标和传感器） 的范围更广的一般性支持。 在 SoC 平台上 HID 设备通过 I2C，可连接到该平台，并由 ACPI 枚举。 对于 Windows 中的 HID 类支持的兼容性，则使用以下命名空间对象：

- 供应商特定\_HID
- 一个\_PNP0C50 CID
- 一个\_CRS 使用：
  - 设备的访问权限 I2CSerialBusConnection 资源
  - Interrupt(s) GpioInt 资源
- HIDI2C \_DSM 方法在设备中返回的 HID 描述符注册地址。 有关详细信息，请参阅[HIDI2C 特定于设备的方法 (\_DSM)](hidi2c-device-specific-method---dsm-.md)。

## <a name="button-devices"></a>按钮的设备

对于 SoC 平台，Windows 支持 ACPI 定义控制方法电源按钮，以及 Windows 兼容五个按钮数组。 电源按钮是否作为 ACPI 控件方法电源按钮或 Windows 兼容按钮数组的一部分实现执行以下操作：

- 会导致平台来强化如果它处于关闭状态。
- 生成时按下电源按钮重写事件。 有关详细信息，请参阅部分 4.8.2.2.1.3，"电源按钮重写"，ACPI 5.0 规范。

### <a name="control-method-power-button"></a>控制方法电源按钮

蛤设计以及使用内置或连接键盘、 其他系统实现 ACPI 定义控制方法电源按钮 （部分 4.8.2.2.1.2 ACPI 5.0 规范的） 使用 GPIO-Signaled ACPI 事件 （5.6.5 ACPI 5.0 规范部分）. 若要支持的电源按钮设备，该命名空间：

- 介绍将作为非共享 （排他） GPIO 的电源按钮 GPIO 中断固定中断资源。
- 列出了中的电源按钮 GPIO 中断资源\_AEI GPIO 控制器连接到的对象。
- 提供了相关联的事件方法 (Lxx/Exx/EVT) GPIO 控制器设备下。 此事件方法通知按钮事件已发生的操作系统中的控制方法按钮驱动程序。

有关详细信息，请参阅[Windows 8 平板电脑和可转换为设备的硬件按钮](https://go.microsoft.com/fwlink/p/?linkid=331284)。

### <a name="windows-compatible-button-array"></a>Windows 兼容按钮数组

对于触摸优先 （无键盘） 平台，例如平板电脑，Windows 提供的通用驱动程序为五个按钮数组。 数组中的每个按钮都定义函数 （请参阅下面的列表中带编号的项），并且某些"保留按"按钮组合在 UI 中具有其他含义。 任何按钮的组合不定义需要按下电源按钮。 与 Windows 收件箱按钮驱动程序的兼容性，为实现 Windows 兼容按钮数组 ACPI 设备。 设备定义，如下所示：

- 五个按钮的每个已连接到在平台上其自己专用的中断 pin。
- 配置每个中断 pin 作为非共享 （专用），edge 触发 (Edge) 中断中断 (ActiveBoth) 这两个边缘的资源。
- 供应商定义的设备命名空间包含\_HID 以及\_CID PNP0C40。
- 中的 GPIO 中断资源\_CRS 对象按以下顺序列出：

    1. 中断对应的"电源"按钮

        "电源"按钮必须支持唤醒的 (ExclusiveAndWake)。

    2. 中断对应于"Windows"按钮

        Windows 按钮必须支持唤醒的 (ExclusiveAndWake)。

    3. 中断对应于"提高音量"按钮

        不能支持唤醒的"提高音量"按钮 （必须使用排他）。

    4. 中断对应于"降低音量"按钮

        "调低音量"按钮不能支持唤醒的 （必须使用排他）。

中断对应于"旋转锁定"按钮，如果受支持

        The "Rotation Lock" button must not be wake-capable (must use Exclusive).

有关详细信息，请参阅[Windows 8 平板电脑和可转换为设备的硬件按钮](https://go.microsoft.com/fwlink/p/?linkid=331284)。

若要支持的 Windows 按钮 UI 演变，Windows 定义了特定于设备的方法 (\_DSM) 的 Windows 按钮数组设备。 有关详细信息，请参阅[Windows 按钮数组特定于设备的方法 (\_DSM)](windows-button-array-device-specific-method---dsm-.md)。

## <a name="dock-and-convertible-pc-sensing-devices"></a>停靠和感知设备的改变 PC

Windows 支持通过在 ACPI 名称空间中的两个花巨资投入设备使用停靠和双用型 (蛤/平板电脑 combos)。 通过 Windows 收件箱按钮驱动程序支持这些设备。 请注意将应用到按钮数组设备相同的要求也适用于这些设备：

- GPIO ActiveBoth 中断必须连接到在 SoC GPIO 控制器 （不到连接存储的 GPIO 控制器）。
- GPIO 控制器必须支持级别模式中断和动态极性重新编程。
- GPIO 控制器驱动程序必须使用提供的 ActiveBoth 仿真[GPIO 框架扩展](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpioclx-i-o-and-interrupt-interfaces)(**GpioClx**)。
- 如果断言的状态 （"停靠"或"Converted"） 没有被声明逻辑级别较低，GPIO 控制器\_DSM 方法需重写 GPIO 驱动程序堆栈的默认行为。 有关详细信息，请参阅**GPIO 控制器设备**主题中[常规用途 I/O (GPIO)](general-purpose-i-o--gpio-.md)主题。

有关详细信息，请参阅[Windows 8 平板电脑和可转换为设备的硬件按钮](https://go.microsoft.com/fwlink/p/?linkid=331284)。

### <a name="dock-sensing-device"></a>停靠感知设备

附加或从系统未附加停靠时，停靠感知设备会中断系统。 此模式下更改信息用于更新用户输入和输出与所需的体验。 设备的命名空间要求：

- 供应商特定\_HID
- 一个\_PNP0C70 CID
- 一个\_CRS 与一个 ActiveBoth 中断

    不能支持唤醒的中断。

### <a name="convertible-pc-sensing-device"></a>可转换为 PC 花巨资投入设备

当转换 PC 从平板电脑切换到蛤外形规格时，可转换为 PC 感知设备中断系统。 此模式下更改信息用于更新用户输入和输出与所需的体验。 设备的命名空间要求：

- 供应商特定\_HID
- 一个\_PNP0C60 CID
- 一个\_CRS 与一个 ActiveBoth 中断

    不能支持唤醒的中断。
