---
title: 使用 GUID_DEVICE_RESET_INTERFACE_STANDARD
description: 使用 GUID_DEVICE_RESET_INTERFACE_STANDARD
keywords:
- GUID_DEVICE_RESET_INTERFACE_STANDARD
ms.date: 11/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30b13eff1d7988e5f18ef23cc2d057b830b749a8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327235"
---
# <a name="working-with-the-guiddeviceresetinterfacestandard"></a>使用 GUID_DEVICE_RESET_INTERFACE_STANDARD

GUID_DEVICE_RESET_INTERFACE_STANDARD 接口定义功能的驱动程序尝试重置并恢复运行不正常设备的标准方法。

通过此接口提供了两个类型的设备重置：

- 函数级设备重置。 在这种情况下，重置操作仅限于特定的设备，并且不到其他设备可见。 设备保持与在重置整个总线的连接，并返回到有效状态 （初始状态） 后重置。 这种类型的重置在系统上具有最小影响。 

- 可以实现这种类型的重置，总线驱动程序或 ACPI 固件。 总线驱动程序可以实现函数级别重置如果总线规范定义了一种带内重置机制，满足的要求。 ACPI 固件可以选择重写由总线驱动程序定义函数级别重置其自己的实现。

平台级别的设备重置。 在这种情况下，重置操作会导致设备被报告为丢失从总线。 重置操作会影响特定设备和所有其他设备通过相同的电源线连接到它或者重设行。 这种类型的重置在系统上具有最大的影响。 操作系统将关闭并重新生成所有受影响的设备以确保所有内容重启从空状态的堆栈。

从 Windows 10，这些注册表项下开始`HKLM\SYSTEM\CurrentControlSet\Control\Pnp`注册表项配置重置操作： 

- DeviceResetRetryInterval:操作会开始重置前的时间段。 默认值为 3 秒。 最小值为 100 毫秒;最大值为 30 秒。 

- DeviceResetMaximumRetries:尝试重置操作次数。 

> [!NOTE]
>  可从 Windows 10 开始 GUID_DEVICE_RESET_INTERFACE_STANDARD 接口。
 

## <a name="using-the-device-reset-interface"></a>使用设备重置接口

如果函数驱动程序检测到，在设备工作不正常，它应首先尝试函数级别重置。 如果函数级别重置未解决此问题，然后可以选择该驱动程序尝试平台级别重置。 但是，应只使用平台级别重置，作为最后一个选项。

若要查询为此接口，设备驱动程序将发送 IRP_MN_QUERY_INTERFACE IRP 关闭驱动程序堆栈。 为此 IRP，驱动程序设置为 GUID_DEVICE_RESET_INTERFACE_STANDARD InterfaceType 输入的参数。 成功完成后的 IRP，接口输出参数是指向 DEVICE_RESET_INTERFACE_STANDARD 结构的指针。 此结构包含可用于请求函数级别或平台级别重置的 DeviceReset 例程的指针。

## <a name="supporting-the-device-reset-interface-in-function-drivers"></a>支持设备重置功能的驱动程序中的接口

若要支持的设备重置接口，设备堆栈必须满足以下要求。

IRP_MN_QUERY_REMOVE_DEVICE、 IRP_MN_REMOVE_DEVICE 和 IRP_MN_SURPRISE_REMOVAL，必须正确处理功能驱动程序。 

在大多数情况下，当驱动程序收到 IRP_MN_QUERY_REMOVE_DEVICE，它应返回成功完成，以便可以安全地删除该设备。 但是，可能有情况下，不能安全地停用设备，例如像设备陷在循环写入内存缓冲区。 在这种情况下，该驱动程序应返回 IRP_MN_QUERY_REMOVE_DEVICE STATUS_DEVICE_HUNG。 PnP 管理器将继续 IRP_MN_QUERY_REMOVE_DEVICE 和 IRP_MN_REMOVE_DEVICE 过程中，但该特定堆栈将不会收到 IRP_MN_REMOVE_DEVICE。 相反，设备堆栈重置设备后会收到 IRP_MN_SURPRISE_REMOVAL。

有关这些 Irp 的详细信息，请参阅： 

[处理一个 IRP_MN_QUERY_REMOVE_DEVICE 请求](handling-an-irp-mn-query-remove-device-request.md)

[处理一个 IRP_MN_REMOVE_DEVICE 请求](handling-an-irp-mn-remove-device-request.md)

[处理一个 IRP_MN_SURPRISE_REMOVAL 请求](handling-an-irp-mn-surprise-removal-request.md)

## <a name="supporting-the-device-reset-interface-in-filter-drivers"></a>支持设备重置筛选器驱动程序中的接口

筛选器驱动程序可能会截获 IRP_MN_QUERY_INTERFACE Irp GUID_DEVICE_RESET_INTERFACE_STANDARD 接口类型。 通过此操作，它们可以继续将委托给 GUID_DEVICE_RESET_INTERFACE_STANDARD 接口，但重置操作之前或之后执行特定于设备的操作。 或者，可以重写以提供其自己重置操作使用其自己的界面总线驱动程序返回的 GUID_DEVICE_RESET_INTERFACE_STANDARD 接口。

## <a name="supporting-the-device-reset-interface-in-bus-drivers"></a>支持设备重置总线驱动程序中的接口

参与设备重置过程 （即，总线驱动程序所带来的请求重置设备） 和总线驱动程序所带来的响应重置请求的设备的总线驱动程序必须满足以下项之一要求：

- 为支持热插拔。 总线驱动程序必须能够检测到正在从恕不另行通知，总线中删除的设备和设备插入到总线。

- 或者，它必须实现 GUID_REENUMERATE_SELF_INTERFACE_STANDARD 接口。 这模拟源自总线和返回连接的设备。 内置的总线驱动程序 （如 PCI 和 SDBUS） 支持此接口。 因此，如果要重置的设备使用这些总线之一，不做任何总线驱动程序修改才不有必要。

有关基于 WDF 的总线驱动程序，WDF 框架将注册 GUID_REENUMERATE_SELF_INTERFACE_STANDARD 接口代表驱动程序。 因此，注册此接口不需要这些驱动程序。 如果需要执行某些操作之前重新枚举其子设备总线驱动程序，它必须注册，以便 EvtChildListDeviceReenumerated 回调例程和该例程中执行的操作。 因为此回调例程中可能调用并行的所有 PDO，该例程中的代码可能需要防止争用条件。

## <a name="acpi-firmware-function-level-reset"></a>ACPI 固件：函数级别重置

若要支持函数级别的设备重置，必须在设备作用域内定义的 _RST 方法。 如果存在，此方法将重写函数级别 （如果存在） 重置该设备的设备的总线驱动程序的实现。 执行时，_RST 方法必须重置仅该设备，并且必须不会影响其他设备。 此外，设备必须保持连接总线上。

## <a name="acpi-firmware-platform-level-reset"></a>ACPI 固件：平台级别重置

若要支持的平台级别的设备重置，有两个选项：

- ACPI 固件可以定义可实现 _RST 方法中，PowerResource 和所有设备受此重置方法可以是都指通过 _PRR 对象在其设备的作用域下定义此 PowerResource。

- 设备可以声明 _PR3 对象。 在这种情况下，ACPI 驱动程序将使用 D3cold power 循环执行重置，并且重置设备之间的依赖项将确定从 _PR3 对象。

如果设备作用域中存在 _PRR 对象，ACPI 驱动程序将使用 _RST 方法中引用 PowerResource 执行重置。 如果没有 _PRR 对象定义但 _PR3 对象定义，ACPI 驱动程序将使用 D3cold power 循环执行重置。 如果定义 _PRR 或 _PR3 既没有对象，则该设备不支持的平台级别重置并且 ACPI 驱动程序将报告的平台级别重置不可用。

### <a name="verifying-acpi-firmware-on-the-test-system"></a>验证测试系统上的 ACPI 固件
若要测试您的驱动程序支持设备重置和恢复，请按照以下过程。 此过程假定您正在使用此示例 ASL 文件。 

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
 


1. 通过使用如 Asl.exe ASL compiler 编译到 AML 测试 ASL 文件。 中的可执行文件包含 Windows Driver Kit (WDK) 中。 

```console
Asl <test>.asl
```

上述命令生成 SSDT.aml。

2. 重命名 acpitabl.dat SSDT.aml。 

3. 复制到测试系统上的 %systemroot%\system32 acpitabl.dat。 

4. 启用测试签名的测试系统上。 

```console
bcdedit /set GUID_DEVICE_RESET_INTERFACE_STANDARD testsigning on
```

5. 重新启动的测试系统。 

6. 验证加载表。 在 Windows 调试器中，使用以下命令。 

- !acpicache 
- dt _DESCRIPTION_HEADER 地址的 SSDT 表 

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

## <a name="see-also"></a>请参阅

[_DEVICE_RESET_INTERFACE_STANDARD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_reset_interface_standard) 

