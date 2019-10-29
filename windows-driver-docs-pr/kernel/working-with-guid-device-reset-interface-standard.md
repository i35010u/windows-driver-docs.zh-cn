---
title: 使用 GUID_DEVICE_RESET_INTERFACE_STANDARD
description: 使用 GUID_DEVICE_RESET_INTERFACE_STANDARD
keywords:
- GUID_DEVICE_RESET_INTERFACE_STANDARD
ms.date: 11/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b326cfab0ac2cff63f0387f2e2c1b68b4085fc9
ms.sourcegitcommit: f8ef49aa583f63edeab42001af8dfb41031ab622
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72998636"
---
# <a name="working-with-the-guid_device_reset_interface_standard"></a>使用 GUID_DEVICE_RESET_INTERFACE_STANDARD

GUID_DEVICE_RESET_INTERFACE_STANDARD 接口定义了一种标准方法，使函数驱动程序可以尝试重置和恢复故障设备。

通过此接口可使用两种类型的设备重置：

- 功能级设备重置。 在这种情况下，重置操作仅限于特定设备，不适用于其他设备。 设备在重置过程中保持连接到总线，并在重置后恢复为有效状态（初始状态）。 这种类型的重置对系统产生的影响最小。 

- 这种类型的重置可通过总线驱动程序或 ACPI 固件实现。 如果总线规范定义满足要求的带内重置机制，则总线驱动程序可以实现函数级重置。 ACPI 固件可以选择性地使用其自己的实现替代总线驱动程序定义的函数级重置。

平台级别设备重置。 在这种情况下，reset 操作会导致从总线将设备报告为缺失。 Reset 操作会影响特定设备以及通过相同的电源导轨或重置线路连接到该设备的所有其他设备。 这种类型的重置对系统产生的影响最大。 操作系统将会断开并重建所有受影响设备的堆栈，以确保所有设备都从空白状态重启。

从 Windows 10 开始，`HKLM\SYSTEM\CurrentControlSet\Control\Pnp` 项下的这些注册表项将配置重置操作： 

- DeviceResetRetryInterval：重置操作开始前的时间段。 默认值为3秒。 最小值为100毫秒;最大值为30秒。 

- DeviceResetMaximumRetries：尝试重置操作的次数。 

> [!NOTE]
>  从 Windows 10 开始，GUID_DEVICE_RESET_INTERFACE_STANDARD 接口可用。
 

## <a name="using-the-device-reset-interface"></a>使用设备重置接口

如果函数驱动程序检测到设备不能正常工作，则应首先尝试函数级重置。 如果函数级重置不能解决问题，则驱动程序可以选择尝试平台级别的重置。 不过，平台级别的重置只应用作最终选项。

若要查询此接口，设备驱动程序会向下发送 IRP_MN_QUERY_INTERFACE IRP 驱动程序堆栈。 对于此 IRP，驱动程序将 InterfaceType 输入参数设置为 GUID_DEVICE_RESET_INTERFACE_STANDARD。 成功完成 IRP 后，接口 output 参数是指向 DEVICE_RESET_INTERFACE_STANDARD 结构的指针。 此结构包含指向 DeviceReset 例程的指针，它可用于请求函数级别或平台级别的重置。

## <a name="supporting-the-device-reset-interface-in-function-drivers"></a>支持功能驱动程序中的设备重置接口

若要支持设备重置接口，设备堆栈必须满足以下要求。

函数驱动程序必须正确处理 IRP_MN_QUERY_REMOVE_DEVICE、IRP_MN_REMOVE_DEVICE 和 IRP_MN_SURPRISE_REMOVAL。 

在大多数情况下，当驱动程序收到 IRP_MN_QUERY_REMOVE_DEVICE 时，它应返回成功，以便可以安全地删除设备。 但是，在某些情况下，无法安全地停止设备，如设备停滞在写入内存缓冲区的循环中。 在这种情况下，驱动程序应将 STATUS_DEVICE_HUNG 返回到 IRP_MN_QUERY_REMOVE_DEVICE。 PnP 管理器将继续执行 IRP_MN_QUERY_REMOVE_DEVICE 和 IRP_MN_REMOVE_DEVICE 进程，但该特定堆栈不会接收 IRP_MN_REMOVE_DEVICE。 设备堆栈会在重置设备后接收 IRP_MN_SURPRISE_REMOVAL。

有关这些 Irp 的详细信息，请参阅： 

[处理 IRP_MN_QUERY_REMOVE_DEVICE 请求](handling-an-irp-mn-query-remove-device-request.md)

[处理 IRP_MN_REMOVE_DEVICE 请求](handling-an-irp-mn-remove-device-request.md)

[处理 IRP_MN_SURPRISE_REMOVAL 请求](handling-an-irp-mn-surprise-removal-request.md)

## <a name="supporting-the-device-reset-interface-in-filter-drivers"></a>支持筛选器驱动程序中的设备重置接口

筛选器驱动程序可能会截获具有 GUID_DEVICE_RESET_INTERFACE_STANDARD 接口类型的 IRP_MN_QUERY_INTERFACE Irp。 这样，他们就可以继续委托到 GUID_DEVICE_RESET_INTERFACE_STANDARD 接口，但在重置操作前后执行特定于设备的操作。 或者，它们可以使用自己的接口替代总线驱动程序返回的 GUID_DEVICE_RESET_INTERFACE_STANDARD 接口，以便提供其自己的重置操作。

## <a name="supporting-the-device-reset-interface-in-bus-drivers"></a>支持总线驱动程序中的设备重置接口

参与设备重置过程的总线驱动程序（即与请求重置的设备关联的总线驱动程序和与响应重置请求的设备关联的总线驱动程序）必须满足以下其中一项要求

- 支持热插拔。 总线驱动程序必须能够检测到在没有通知的情况下从总线中删除的设备，以及插入总线的设备。

- 或者，它必须实现 GUID_REENUMERATE_SELF_INTERFACE_STANDARD 接口。 这会模拟从总线请求并插回的设备。 内置总线驱动程序（如 PCI 和 SDBUS）支持此接口。 因此，如果要重置的设备使用这些总线之一，则不需要进行任何总线驱动程序修改。

对于基于 WDF 的总线驱动程序，WDF 框架代表驱动程序注册 GUID_REENUMERATE_SELF_INTERFACE_STANDARD 接口。 因此，不需要为这些驱动程序注册此接口。 如果在重新枚举子设备之前，总线驱动程序需要执行某些操作，则它必须注册 EvtChildListDeviceReenumerated 回调例程并在该例程中执行这些操作。 由于可以对所有 PDO 并行调用此回调例程，因此，例程中的代码可能需要防止争用条件。

## <a name="acpi-firmware-function-level-reset"></a>ACPI 固件：功能级重置

若要支持功能级别的设备重置，必须在设备范围内定义 _RST 方法。 如果存在此方法，则此方法将重写总线驱动程序对该设备的函数级别设备重置（如果存在）的实现。 执行时，_RST 方法只能重置该设备，而不能影响其他设备。 此外，设备必须在总线上保持连接状态。

## <a name="acpi-firmware-platform-level-reset"></a>ACPI 固件：平台级别的重置

为了支持平台级别的设备重置，有两个选项：

- ACPI 固件可以定义一个实现 _RST 方法的 PowerResource，受此 reset 方法影响的所有设备都可以通过其设备范围内定义的 _PRR 对象来引用此 PowerResource。

- 设备可以声明 _PR3 对象。 在这种情况下，ACPI 驱动程序将使用 D3cold 电源循环来执行重置，并从 _PR3 对象确定设备之间的依赖关系。

如果 _PRR 对象存在于设备范围内，ACPI 驱动程序将使用引用的 PowerResource 中的 _RST 方法执行重置。 如果未定义任何 _PRR 对象，但定义了 _PR3 对象，则 ACPI 驱动程序将使用 D3cold 电源循环来执行重置。 如果 _PRR 或 _PR3 对象均未定义，则设备不支持平台级重置，并且 ACPI 驱动程序将报告平台级别的重置不可用。

### <a name="verifying-acpi-firmware-on-the-test-system"></a>验证测试系统上的 ACPI 固件
若要测试支持设备重置和恢复的驱动程序，请按照此过程操作。 此过程假定你使用的是此示例 ASL 文件。 

 ```asl
DefinitionBlock("SSDT.AML", "SSDT", 0x01, "XyzOEM", "TestTabl", 0x00001000)
{
    Scope(\_SB_)
       {
        PowerResource(PWFR, 0x5, 0x0)
        {
            Method(_RST, 0x0, NotSerialized)    { }
            
            // Placeholder methods as power resources need _ON, _OFF, _STA.
            Method(_STA, 0x0, NotSerialized)
            {
                Return(0xF)
            }

            Method(_ON_, 0x0, NotSerialized)    { }

            Method(_OFF, 0x0, NotSerialized)    { }

        } // PowerResource()
    } // Scope (\_SB_)

    // Assumes WiFi device is declared under \_SB.XYZ.
    Scope(\_SB_.XYZ.WIFI)
        {

        // Declare PWFR as WiFi reset power rail
        Name(_PRR, Package(One)
            {
                \_SB_.PWFR
            })
        } // Scope (\_SB)
}
```
 


1. 使用 ASL 编译器（如 Asl）将测试 ASL 文件编译为 AML。 Windows 驱动程序工具包（WDK）中包含的可执行文件。 

```console
Asl <test>.asl
```

前面的命令生成 SSDT。

2. 将 SSDT 重命名为 acpitabl。 

3. 将 acpitabl 复制到测试系统上的%systemroot%\system32。 

4. 在测试系统上启用测试签名。 

```console
bcdedit /set testsigning on
```

5. 重新启动测试系统。 

6. 验证是否已加载表。 在 Windows 调试器中，使用以下命令。 

- !acpicache 
- SSDT 表的 dt _DESCRIPTION_HEADER 地址 

```dbgcmd
0: kd> !acpicache
Dumping cached ACPI tables...
  SSDT @(ffffffffffd03018) Rev: 0x1 Len: 0x000043 TableID: TestTabl
  XSDT @(ffffffffffd05018) Rev: 0x1 Len: 0x000114 TableID: HSW-FFRD
       ...
       ...
 
0: kd> dt _DESCRIPTION_HEADER ffffffffffd03018
ACPI!_DESCRIPTION_HEADER
   +0x000 Signature        : 0x54445353
   +0x004 Length           : 0x43
   +0x008 Revision         : 0x1 ''
   +0x009 Checksum         : 0x37 '7'
   +0x00a OEMID            : [6]  "XyzOEM"
   +0x010 OEMTableID       : [8]  "TestTabl"
   +0x018 OEMRevision      : 0x1000
   +0x01c CreatorID        : [4]  "MSFT"
   +0x020 CreatorRev       : 0x5000000
```

## <a name="see-also"></a>另请参阅

[_DEVICE_RESET_INTERFACE_STANDARD](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_reset_interface_standard) 

