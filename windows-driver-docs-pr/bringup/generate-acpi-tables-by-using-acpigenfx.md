---
title: 使用 AcpiGenFx 生成 ACPI 表
description: 使用 ACPI 生成框架 (AcpiGenFx) 库来编写用于生成 ACPI 表的应用程序。
ms.date: 09/23/2020
ms.localizationpriority: medium
ms.openlocfilehash: 3f40144b1f1287f9d474e02ccf8044b1bded7ba1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803349"
---
# <a name="generate-acpi-tables-by-using-acpigenfx"></a>使用 AcpiGenFx 生成 ACPI 表

> [!NOTE]
> Microsoft 支持各种不同的环境。 本文介绍了 Microsoft [风格的无偏差通信的 Microsoft 风格指南](/style-guide/bias-free-communication) 的术语参考。 本文中使用的词或短语的一致性是因为它当前出现在软件中。 当软件更新为删除语言时，本文将更新为对齐。

## <a name="summary"></a>总结

- 创建使用 AcpiGenFx 生成 ACPI 表的 .NET 应用

## <a name="applies-to"></a>适用于

- Windows 10

- Windows SoC 和平台引入

## <a name="important-apis"></a>重要的 API

- 在对象浏览器中打开 AcpiGenFx

- 使用 Visual Studio 中的 IntelliSense 功能确定方法和属性

使用 ACPI 生成框架 (AcpiGenFx) 库来编写用于生成 ACPI 表的应用程序。

在 Windows 10 中，新的 c # 库 AcpiGenFx 使你可以更轻松地编写应用程序，用于创建用于描述平台上的硬件设备和资源的 ACPI 表，如中断控制器、SD 主机控制器、GPIO 和 I<sup>2</sup>C 设备。 通过使用框架对象公开的方法和属性，可以描述设备、资源和依赖关系，而无需知道 ACPI 表的确切语法或引用 ACPI 规范。 AcpiGenFx 会生成 ACPI 计算机语言 (ASL 独立于操作系统的) 代码，它还知道特定于 Windows 的要求。

该应用基于这些说明生成相关 ACPI 表文件 (\* aslc 和 \* asl) 。 在生成时，AcpiGenFx 以静态方式分析平台说明，检测循环或未解析的依赖项、设备命名和 UUID 冲突、资源到控制器映射等错误。 因此，生成的 ASL 代码更易于调试，因为 AcpiGenFx 检查最常见的错误，并抽象唯一的 ACPI 实现细节。

AcpiGenFx 在本质上是声明性的：其输出仅为静态数据，而不是用于生成动态运行时方法的。 如果框架未涵盖用例，如先进的外部设备电源管理，则这些方法必须在 Windows 平台扩展驱动程序中实现，或手动添加到 AcpiGenFx 生成的 ASL 代码。

## <a name="before-you-begin"></a>在开始之前

在 WDK 安装的 **AcpiGenFx** 文件夹中找到以下文件。

> [!NOTE]
> 在 WDK 的 "工具" 文件夹中提供 AcpiGenFx.dll 和相关的示例。 在 "工具" 目录中，导航到 "目标体系结构" 文件夹，然后导航到 "AcpiGenFx" 文件夹。 例如，x86 版本位于 C:\Program Files (x86) \Windows Kits\10\Tools\x86\ACPIGenFx。

- AcpiGenFx.dll

    需要使用 ACPIGenFx。

- DSDTSamples

    使用此项目作为为整个平台设计 ACPI 固件的起点。 输出是一组包含 DSDT、FADT 和 MADT 的完整 ACPI 表。

- SSDTSamples

    使用此项目作为将外围设备添加到现有系统的起点。 此示例演示如何描述传感器设备及其资源。 输出是 ASL 中的 ACPI SSDT 表。

下载 Windows 10 工具包、工具和代码示例。

- [Microsoft Visual Studio](https://visualstudio.microsoft.com/)

- [适用于 Windows 10 的 windows 驱动程序工具包 (WDK) ](../download-the-wdk.md)

- [Windows 驱动程序工具包 (WDK) 示例](https://github.com/Microsoft/Windows-driver-samples)

## <a name="create-a-platform"></a>创建平台

1. 在 Visual Studio 中，打开一个新的 c # 控制台项目。

1. 向 AutoAcpi.dll 程序集添加引用。 在 " **项目** " 菜单下，单击 " **添加引用**"。 单击 " **浏览** " 并导航到 AutoAcpi.dll 的位置。 单击 **“确定”** 。

1. 在 **解决方案资源管理器** 中，展开 " **引用** " 并选择 " **acpigenfx**"。 查看对象浏览器 (**视图 &gt; 对象浏览器**) 中的对象。

1. 目标 .NET Framework 4.5 或更高版本。 打开项目属性。 在 " **应用程序** " 页上，确保 " **目标框架** " 设置为 **.NET Framework 4.5**。

1. `Using`在应用程序的代码开头添加 AutoAcpi 对象的指令。

1. 创建平台对象。 根据你的体系结构，通过调用 **CreateArmPlatform** 或 **Createx86Platform** 实例化 **平台** 对象。 指定 *OEMID*、 *OEMTableID*、 *Creator*、 *Revision* 和 *FileName*。

1. 调用 **WriteAsl** 以写入文件。

    此示例演示如何实例化平台。

    ```cs
    using AutoAcpi;

    namespace ACPI
    {
        class Program
        {
            static void Main(string[] args)
            {
                ArmPlatform myPlatform = Platforms.CreateArmPlatform(
                    OEMID: "MSFT",
                    OEMTableID: "EDK2",
                    CreatorID: "MSFT",
                    Revision: 1,
                    FileName: "Platform");

                myPlatform.WriteAsl();
            }
        }
    }
    ```

1. 单击 " **开始** " 生成并运行应用。 Visual Studio 会在 " **输出** " 窗口中显示生成进度。  (如果 "**输出**" 窗口不可见，请从 "**视图**" 菜单中选择 "**输出**"。 ) 。

1. 打开名为 "*项目* \\ bin \\ *调试" 或 "发布* 输出" 的文件夹 \\ 。 Output 文件夹包含由应用程序生成的文件。 查看 SSDT. asl 的内容。

    下面是前面示例的输出。

    ```console
    DefinitionBlock ("Platform.aml", "DSDT", 5, "MSFT", "EDK2", 1)
    {
        Scope (\_SB_)
        {
        }

    }
    ```

该应用程序会生成两个其他文件夹： Aslc 和 Bin。 Aslc 包含 Aslc 格式的所有固件表。 Bin 包含二进制 blob 格式的所有固件表。

使用 WDK 中提供的 asl.exe 编译器，将 ASL 代码文件编译为 ACPI 计算机语言 (AML) 二进制。

## <a name="add-devices-and-resources-in-the-dsdt"></a>在 DSDT 中添加设备和资源

可以将组件添加到平台。 通常，这些组件包括处理器、总线控制器、电源资源等。 下面是 DSDTSamples 中使用的一些组件。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>对象类型</th>
<th>创建方法</th>
<th>组件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>ACAdapter</strong></td>
<td><strong>AddACAdapter</strong></td>
<td>添加交流适配器。</td>
</tr>
<tr class="even">
<td><strong>BatteryDevice</strong></td>
<td><p><strong>AddBatteryDevice</strong></p>
<p><strong>BatteryDevice.ThermalLimit</strong></p></td>
<td>添加电池设备并指定其温度限制。</td>
</tr>
<tr class="odd">
<td><strong>ButtonArrayDevice</strong></td>
<td><p><strong>AddButtonArrayDevice</strong></p>
<p><strong>ButtonArrayDevice.AddBackButton</strong></p>
<p><strong>ButtonArrayDevice.AddCameraShutterButton</strong></p>
<p><strong>ButtonArrayDevice.AddCameraAutofocusButton</strong></p>
<p><strong>ButtonArrayDevice.AddGenericButton</strong></p>
<p><strong>ButtonArrayDevice.AddPowerButton</strong></p>
<p><strong>ButtonArrayDevice.AddRotationLockButton</strong></p>
<p><strong>ButtonArrayDevice.AddSearchButton</strong></p>
<p><strong>ButtonArrayDevice.AddVolumeDownButton</strong></p>
<p><strong>ButtonArrayDevice.AddVolumeUpButton</strong></p>
<p><strong>ButtonArrayDevice.AddWindowsHomeButton</strong></p></td>
<td>添加按钮，如 Windows Home、Back、Volume +/-、Power、旋转锁定和搜索。</td>
</tr>
<tr class="even">
<td><strong>DisplaySensor</strong></td>
<td><strong>AddDisplaySensor</strong></td>
<td>添加显示传感器。</td>
</tr>
<tr class="odd">
<td><strong>GenericDevice</strong></td>
<td><strong>AddGenericDevice</strong></td>
<td>添加可用于在框架中替换任意类型的内部支持设备的通用设备。</td>
</tr>
<tr class="even">
<td><strong>GpioController</strong></td>
<td><strong>AddGpioController</strong></td>
<td>添加 GPIO 控制器和相关资源，如中断、i/o 和事件。</td>
</tr>
<tr class="odd">
<td><strong>HidOverI2C</strong></td>
<td><strong>AddHidI2CDevice</strong></td>
<td>添加连接到 I<sup>2</sup>C 总线的 HID 设备。</td>
</tr>
<tr class="even">
<td><strong>I2CController</strong></td>
<td><strong>AddI2CController</strong></td>
<td>添加 I<sup>2</sup>个 C 控制器和相关资源，例如中断、i/o 和事件。</td>
</tr>
<tr class="odd">
<td><strong>KDNet2Usb</strong></td>
<td><strong>AddKDNet2Usb</strong></td>
<td>通过使用 Kdnet over USB 来添加对内核调试的支持。</td>
</tr>
<tr class="even">
<td><strong>PEPDevice</strong></td>
<td><strong>AddPepDevice</strong></td>
<td>添加 PEP 设备及其资源和返回包和静态类型的方法。</td>
</tr>
<tr class="odd">
<td><p><strong>处理器</strong></p>
<p><strong>ProcessorAggregator</strong></p></td>
<td><p><strong>AddProcessor</strong></p>
<p><strong>AddProcessorAggregator</strong></p></td>
<td>添加处理器和处理器聚合。</td>
</tr>
<tr class="even">
<td><strong>RTCDevice</strong></td>
<td><strong>AddRTCDevice</strong></td>
<td>添加 ACPI 时间和警报设备。</td>
</tr>
<tr class="odd">
<td><strong>SdHostController</strong></td>
<td><strong>AddSdHostController</strong></td>
<td>添加 SD 主机控制器。</td>
</tr>
<tr class="even">
<td><strong>SerialPort</strong></td>
<td><strong>AddSerialPort</strong></td>
<td>添加对串行和 UART 设备的支持。</td>
</tr>
<tr class="odd">
<td><strong>ThermalZone</strong></td>
<td><strong>AddThermalZone</strong></td>
<td>添加热量区域、相关采样和轮询周期。</td>
</tr>
<tr class="even">
<td><p><strong>XhciUsbController</strong></p>
<p><strong>EhciUsbController</strong></p>
<p><strong>UsbDevice</strong></p></td>
<td><p><strong>AddEhciUsbController</strong></p>
<p><strong>AddXhciUsbController</strong></p>
<p><strong>EhciUsbController.AddUsbDevice</strong></p>
<p><strong>XhciUsbController.AddUsbDevice</strong></p>
<p><strong>UsbDevice.AddUsbDevice</strong></p></td>
<td>添加 USB 主机控制器和子设备 (包括集线器) 。</td>
</tr>
</tbody>
</table>

若要查看完整列表，请在 **对象浏览器** 中打开 AcpiGenFx。 使用 IntelliSense 确定 (的方法和这些对象公开的参数) 和属性。 有关演示如何添加类并设置上表中列出的属性的示例代码，请参阅 DSDTSamples 项目。

## <a name="add-debug-support"></a>添加调试支持

若要将端口设置为可调试，请将对象的 **DebugEnabled** 属性设置为 "true"。

例如，你可能想要使用 USB 调试端口来描述 xHCI 主机控制器。 在应用程序中，调用 **AddXhciUsbController** 以获取 **XhciUsbController** 对象，并将 **DebugEnabled** 属性设置为 "true"。 AcpiGenFx 生成将自动包含在应用的 Output Aslc 文件夹中的 Microsoft DBG2 表 \\ 。

下面的示例演示如何添加 xHCI 主机控制器并将其声明为可调试。

```cs

XhciUsbController usb1 = Platform.AddXhciUsbController("USB1", "XHCICONT", 0);
usb1.Description = "USB Controller with Debug Support";

Memory32Fixed mem = usb1.AddMemory32Fixed(true, 0xf9000000, 0xfffff, "");
usb1.AddMemory32Fixed(true, 0xf7000000, 0xfffff, "");
usb1.AddInterrupt(InterruptType.Level, InterruptActiveLevel.ActiveHigh, SharingLevel.Shared, 0x8);
usb1.AddInterrupt(InterruptType.Level, InterruptActiveLevel.ActiveHigh, SharingLevel.Shared, 0x9);

usb1.DebugEnabled = true;
mem.DebugAccessSize = DebugAccessSize.DWordAccess;
```

在上述代码片段中，xHCI 主机控制器具有中断资源和调试支持。 它在 PEP 设备和 GPIO 控制器上具有依赖关系。 若要查看这些设备的说明，请参阅 DSDTSamples。

此示例演示如何将 I<sup>2</sup>C 控制器添加到 DSDT。

```cs
I2CController i2c = Platform.AddI2CController("I2C1", "I2CCONTR", 0);
i2c.AddMemory32Fixed(true, 0xf9999000, 0x400, "");
i2c.AddInterrupt(InterruptType.Level, InterruptActiveLevel.ActiveHigh, SharingLevel.Exclusive, 40);
```

下面是包含 xHCI host 和 I<sup>2</sup>C 控制器定义的控制台应用的输出。

```console

DefinitionBlock ("Platform.aml", "DSDT", 5, "MSFT", "EDK2", 1)
{
    Scope (\_SB_)
    {
        //
        // Description: USB Controller with Debug Support
        //

        Device (USB1)
        {
            Name (_HID, "XHCICONT")
            Name (_CID, "PNP0D10")
            Name (_UID, 0x0)
            Method (_STA)
            {
                Return(0xf)
            }
            Method (_CRS, 0x0, NotSerialized) {
                Name (RBUF, ResourceTemplate () {
                    MEMORY32FIXED(ReadWrite, 0xF9000000, 0xFFFFF, )
                    MEMORY32FIXED(ReadWrite, 0xF7000000, 0xFFFFF, )
                    Interrupt(ResourceConsumer, Level, ActiveHigh, Shared) { 0x8 }
                    Interrupt(ResourceConsumer, Level, ActiveHigh, Shared) { 0x9 }
                })
                Return(RBUF)
            }
        }

        //
        // Description: This is an i2cController.
        //

        Device (I2C1)
        {
            Name (_HID, "I2CCONTR")
            Name (_CID, "")
            Name (_UID, 0x0)
            Method (_STA)
            {
                Return(0xf)
            }
            Method (_CRS, 0x0, NotSerialized) {
                Name (RBUF, ResourceTemplate () {
                    MEMORY32FIXED(ReadWrite, 0xF9999000, 0x400, )
                    Interrupt(ResourceConsumer, Level, ActiveHigh, Exclusive) { 0x28 }
                })
                Return(RBUF)
            }
        }

    }

}  
```

生成项目后，在项目目录中，导航到 Output \\ Aslc。 Dbg2. aslc 文件包含如下所示的 DB2 表：

```asl

// Debug Port Table (DBG2)
// Automatically generated by AutoAcpi

#include "AutoACPI.h"
char DBG2[112] = {
    0x44, 0x42, 0x47, 0x32, 0x70, 0x00, 0x00, 0x00, 0x00, 0x00,
    0x4D, 0x53, 0x46, 0x54, 0x20, 0x20, 0x45, 0x44, 0x4B, 0x32,
    0x20, 0x20, 0x20, 0x20, 0x01, 0x00, 0x00, 0x00, 0x4D, 0x53,
    0x46, 0x54, 0x01, 0x00, 0x00, 0x00, 0x2C, 0x00, 0x00, 0x00,
    0x01, 0x00, 0x00, 0x00, 0x00, 0x44, 0x00, 0x02, 0x0E, 0x00,
    0x36, 0x00, 0x00, 0x00, 0x44, 0x00, 0x02, 0x80, 0x00, 0x00,
    0x00, 0x00, 0x16, 0x00, 0x2E, 0x00, 0x00, 0x00, 0x00, 0x03,
    0x00, 0x00, 0x00, 0xF9, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
    0x00, 0x01, 0x00, 0x00, 0x00, 0xF7, 0x00, 0x00, 0x00, 0x00,
    0xFF, 0xFF, 0x0F, 0x00, 0xFF, 0xFF, 0x0F, 0x00, 0x22, 0x5C,
    0x5C, 0x5F, 0x53, 0x42, 0x5F, 0x2E, 0x55, 0x53, 0x42, 0x31,
    0x22, 0x00
};

void * ReferenceDBG2Table(void) {
    return (void *) &DBG2;
}
```

## <a name="add-an-acpi-description-for-a-peripheral-device-in-the-ssdt"></a>为 SSDT 中的外围设备添加 ACPI 说明

1. 通过调用 **CreateArmPlatform** 或 **Createx86Platform** 创建平台对象。

1. 将 **SSDT** 属性设置为 true。 这向框架表明，此表是 SSDT。

1. 创建设备并分配资源。 例如，对于此处显示的传感器设备，示例将调用 **AddGenericDevice** ，并指定设备名称、硬件 ID 和唯一实例。 连接到 I<sup>2</sup>C 串行总线 I2C1 的传感器设备，如 DSDT 中所述。

```asl
namespace SSDTSample
{
    class Program
    {
        static void Main(string[] args)
        {

          ArmPlatform Platform = Platforms.CreateArmPlatform(
                OEMID: "MSFT",
                OEMTableID: "EDK2",
                CreatorID: "MSFT",
                Revision: 1,
                FileName: "SSDT"
                );

            platform.SSDT = true;

            var sensor = platform.AddGenericDevice("ADXL", "ACPI\\ADXL345Acc", 1);

            sensor.AddI2CSerialBus(
                SlaveAddress: 0x1d,
                Mode: SlaveMode.ControllerInitiated,
                ConnectionSpeed: 400000,
                addressmode: AddressMode._7Bit,
                controllername: "I2C1"
                );

            platform.WriteAsl();

        }
    }
}
```

下面是前面示例的输出。

```console
DefinitionBlock ("SSDT.aml", "SSDT", 5, "MSFT", "EDK2", 1)
{
    Scope (\_SB_)
    {

        Device (ADXL)
        {
            Name (_HID, "ACPI\ADXL345Acc")
            Name (_UID, 0x1)
            Method (_STA)
            {
                Return(0xf)
            }
            Method (_CRS, 0x0, NotSerialized) {
                Name (RBUF, ResourceTemplate () {
                    I2CSerialBus(0x1D, ControllerInitiated, 0x61A80, AddressingMode7Bit, "I2C1", 0, ResourceConsumer, , RawDataBuffer() { 0 })
                })
                Return(RBUF)
            }
        }

    }

}
```

## <a name="replacing-acpi-firmware-during-development-and-testing"></a>在开发和测试期间替换 ACPI 固件

在开发和测试方案中，可以替换从设备上的 asl.exe 编译器生成的 AML 二进制文件。 为此，请将 AML 二进制文件重命名为 acpitabl，并将其移动到% windir% \\ system32。 在启动时，Windows 会将 ACPI 固件中存在的表替换为 acpitabl 中的表。

请确保通过命令启用测试签名：

```console
bcdedit /set testsigning on
```

## <a name="related-topics"></a>相关主题

[ACPI 系统说明表](acpi-system-description-tables.md)
