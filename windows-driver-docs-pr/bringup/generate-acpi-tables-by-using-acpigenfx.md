---
title: 使用 AcpiGenFx 生成 ACPI 表
description: 使用 ACPI 生成框架 (AcpiGenFx) 库编写的应用可生成 ACPI 表。
ms.assetid: 46A725C3-609E-45B9-A4BD-033656208E92
ms.date: 06/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7efa87cc6abe752b1692adcc88b62426aeca797e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337600"
---
# <a name="generate-acpi-tables-by-using-acpigenfx"></a>使用 AcpiGenFx 生成 ACPI 表


**摘要**

-   创建使用 AcpiGenFx ACPI 表生成一个.NET 应用

**适用于**

-   Windows 10
-   Windows SoC 和平台提出

**重要的 Api**

-   在对象浏览器中打开 AcpiGenFx
-   使用 Visual Studio 中的 IntelliSense 功能来确定方法和属性

使用 ACPI 生成框架 (AcpiGenFx) 库编写的应用可生成 ACPI 表。

在 Windows 10 中，新C#库，AcpiGenFx，使你更轻松地编写应用程序创建平台，如中断控制器 GPIO，在 SD 主机控制器描述的硬件设备和资源的 ACPI 表和 I²C 设备。 通过使用的方法和属性公开的 framework 对象，可以无需知道 ACPI 表的确切语法或引用的 ACPI 规范描述设备、 资源和依赖项。 AcpiGenFx 不仅生成的是独立于 OS 的 ACPI 机器语言 (ASL) 代码也已考虑到特定于 Windows 的要求。

应用会生成相关的 ACPI 表文件 (\*.aslc 和\*.asl) 根据这些说明。 在生成时，AcpiGenFx 静态分析平台说明中，检测错误，如循环或无法解析依赖项、 设备命名和 UUID 冲突、 控制器映射到的资源以及更多内容。 因此，生成的 ASL 代码容易调试，因为 AcpiGenFx 检查的最常见的错误和摘要唯一 ACPI 实现详细信息。

AcpiGenFx 是声明性本质上： 其输出是只将静态数据，而不是生成动态运行时方法。 如果用例未涵盖的框架，例如高级关闭 SoC 外围设备电源管理，方法必须是 Windows 平台扩展驱动程序中实现或手动添加到 AcpiGenFx 生成 ASL 代码。

## <a name="before-you-begin"></a>开始之前...

找到以下文件中的**AcpiGenFx** WDK 安装文件夹。

> [!NOTE]
> AcpiGenFx.dll 和关联的示例中提供了 WDK 的工具文件夹。 在工具目录中，导航到目标体系结构文件夹，然后 AcpiGenFx 文件夹。 例如，x86 版本位于 C:\Program Files (x86) \Windows Kits\10\Tools\x86\ACPIGenFx。

-   AcpiGenFx.dll

    需要使用 ACPIGenFx。

-   DSDTSamples

    使用此项目作为起点来设计整个平台的 ACPI 固件。 输出是一套完整的 ACPI 表包括 DSDT、 FADT 和 MADT。

-   SSDTSamples

    使用此项目作为起始点添加到现有系统的外围设备。 此示例演示如何描述传感器设备和其资源。 输出是 ASL 中的 ACPI SSDT 表。

下载 Windows 10 的工具包、 工具和代码示例。

-   [Microsoft Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=533470)
-   [适用于 Windows 10 的 Windows 驱动程序工具包 (WDK)](https://go.microsoft.com/fwlink/p/?LinkId=733614)

## <a name="create-a-platform"></a>创建一个平台


1.  在 Visual Studio 中，打开一个新C#控制台项目。
2.  添加对 AutoAcpi.dll 程序集的引用。 下**项目**菜单上，单击**添加引用**。 单击**浏览**并导航到 AutoAcpi.dll 的位置。 单击 **“确定”**。
3.  在中**解决方案资源管理器**，展开**引用**，然后选择**acpigenfx**。 在对象浏览器中查看的对象 (**视图&gt;对象浏览器**)。
4.  面向.NET Framework 4.5 或更高版本。 打开项目属性。 上**应用程序**页面上，确保**目标框架**设置为 **.NET Framework 4.5**。
5.  添加`Using`AutoAcpi 对象的应用程序的代码开始处的指令。
6.  创建平台对象。 根据您的体系结构，实例化**平台**对象通过调用**Platform.CreateArmPlatform**或**Platform.Createx86Platform**。 指定*OEMID*， *OEMTableID*，*创建者*，*修订*，并*文件名*。
7.  调用**Platform.WriteAsl**写入到文件。

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

8.  单击**启动**生成并运行您的应用程序。 Visual Studio 显示生成进度**输出**窗口。 (如果**输出**窗口不可见，请选择**输出**从**视图**菜单。)。
9.  打开文件夹下名为*项目*\\bin\\*调试或发布*\\输出。 输出文件夹包含由应用生成的文件。 查看 SSDT.asl 的内容。

    下面是上述示例的输出。

    ```console
    DefinitionBlock ("Platform.aml", "DSDT", 5, "MSFT", "EDK2", 1)
    { 
        Scope (\_SB_)
        {
        }

    } 
    ```

应用程序生成其他两个文件夹：Aslc 和 Bin。 Aslc 包含 aslc 格式中的所有固件表。 Bin 包含二进制 blob 格式中的所有固件表。

使用 WDK 中提供 asl.exe 编译器编译 ASL 代码文件到 ACPI 机器语言 (AML) 二进制。

## <a name="add-devices-and-resources-in-the-dsdt"></a>在 DSDT 中添加设备和资源


可以将组件添加到该平台。 通常情况下，这些组件包括处理器、 总线控制器、 power 资源等。 下面是一些在 DSDTSamples 中使用的组件。

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
<td><strong>Platform.AddACAdapter</strong></td>
<td>添加交流电适配器。</td>
</tr>
<tr class="even">
<td><strong>BatteryDevice</strong></td>
<td><p><strong>Platform.AddBatteryDevice</strong></p>
<p><strong>BatteryDevice.ThermalLimit</strong></p></td>
<td>添加电池设备，并指定其散热限制。</td>
</tr>
<tr class="odd">
<td><strong>ButtonArrayDevice</strong></td>
<td><p><strong>Platform.AddButtonArrayDevice</strong></p>
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
<td>添加按钮，如 Windows Home 返回，+ /-，电源、 旋转锁和搜索的卷。</td>
</tr>
<tr class="even">
<td><strong>DisplaySensor</strong></td>
<td><strong>Platform.AddDisplaySensor</strong></td>
<td>添加显示传感器。</td>
</tr>
<tr class="odd">
<td><strong>GenericDevice</strong></td>
<td><strong>Platform.AddGenericDevice</strong></td>
<td>添加可用于替换为任何类型的内部支持 framework 中的设备的通用设备。</td>
</tr>
<tr class="even">
<td><strong>GpioController</strong></td>
<td><strong>Platform.AddGpioController</strong></td>
<td>添加 GPIO 控制器和关联的资源，如中断、 I/O 和事件。</td>
</tr>
<tr class="odd">
<td><strong>HidOverI2C</strong></td>
<td><strong>Platform.AddHidI2CDevice</strong></td>
<td>添加连接到 I²C 总线 HID 设备。</td>
</tr>
<tr class="even">
<td><strong>I2CController</strong></td>
<td><strong>Platform.AddI2CController</strong></td>
<td>添加 I²C 控制器和关联的资源，如中断、 I/O 和事件。</td>
</tr>
<tr class="odd">
<td><strong>KDNet2Usb</strong></td>
<td><strong>Platform.AddKDNet2Usb</strong></td>
<td>添加对使用通过 USB Kdnet 内核调试支持。</td>
</tr>
<tr class="even">
<td><strong>PEPDevice</strong></td>
<td><strong>Platform.AddPepDevice</strong></td>
<td>添加 PEP 设备和其资源并返回包和静态类型的方法。</td>
</tr>
<tr class="odd">
<td><p><strong>处理器</strong></p>
<p><strong>ProcessorAggregator</strong></p></td>
<td><p><strong>Platform.AddProcessor</strong></p>
<p><strong>Platform.AddProcessorAggregator</strong></p></td>
<td>添加处理器和处理器聚合器。</td>
</tr>
<tr class="even">
<td><strong>RTCDevice</strong></td>
<td><strong>Platform.AddRTCDevice</strong></td>
<td>添加 ACPI 时间和警报的设备。</td>
</tr>
<tr class="odd">
<td><strong>SdHostController</strong></td>
<td><strong>Platform.AddSdHostController</strong></td>
<td>添加 SD 主控制器。</td>
</tr>
<tr class="even">
<td><strong>SerialPort</strong></td>
<td><strong>Platform.AddSerialPort</strong></td>
<td>添加对序列和 UART 设备的支持。</td>
</tr>
<tr class="odd">
<td><strong>ThermalZone</strong></td>
<td><strong>Platform.AddThermalZone</strong></td>
<td>添加热区域和关联的采样和的轮询周期。</td>
</tr>
<tr class="even">
<td><p><strong>XhciUsbController</strong></p>
<p><strong>EhciUsbController</strong></p>
<p><strong>UsbDevice</strong></p></td>
<td><p><strong>Platform.AddEhciUsbController</strong></p>
<p><strong>Platform.AddXhciUsbController</strong></p>
<p><strong>EhciUsbController.AddUsbDevice</strong></p>
<p><strong>XhciUsbController.AddUsbDevice</strong></p>
<p><strong>UsbDevice.AddUsbDevice</strong></p></td>
<td>添加 USB 主控制器和子设备 （包括中心）。</td>
</tr>
</tbody>
</table>



若要查看完整列表，请打开在 AcpiGenFx**对象浏览器**。 使用 IntelliSense 来确定方法 （和参数） 和由对象公开的属性。 有关示例代码演示如何添加类和在前面的表中，设置列出的属性引用 DSDTSamples 项目。
## <a name="add-debug-support"></a>添加调试支持


若要将端口设置为可调试，设置**DebugEnabled**上为"true"的对象的属性。

例如，你可能想要描述 xHCI 主控制器使用 USB 调试端口。 在应用中，调用**Platform.AddXhciUsbController**若要获取**XhciUsbController**对象，并将**DebugEnabled**属性设置为"true"。 AcpiGenFx 生成自动应用的输出中包含一个 Microsoft DBG2 表\\Aslc 文件夹。

下面是如何添加 xHCI 主控制器并将其声明为可调试的示例。

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

在以上片段中，xHCI 主控制器具有中断资源和调试支持。 它具有 PEP 设备和 GPIO 控制器的依赖项。 若要查看这些设备的说明，请参阅 DSDTSamples。

此示例演示如何将 I²C 控制器添加到 DSDT。

```cs
I2CController i2c = Platform.AddI2CController("I2C1", "I2CCONTR", 0);
i2c.AddMemory32Fixed(true, 0xf9999000, 0x400, "");
i2c.AddInterrupt(InterruptType.Level, InterruptActiveLevel.ActiveHigh, SharingLevel.Exclusive, 40);
```

下面是使用 xHCI 主机和 I²C 控制器的前面定义控制台应用程序的输出。

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

在后生成项目时，项目目录中导航到输出\\Aslc。 Dbg2.aslc 文件包含如下所示的 DB2 表：

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

## <a name="add-an-acpi-description-for-a-peripheral-device-in-the-ssdt"></a>在 SSDT 中添加外围设备的 ACPI 描述


1.  创建平台对象通过调用**Platform.CreateArmPlatform**或**Platform.Createx86Platform**。
2.  设置**SSDT**属性设为 true。 这指示该框架，此表是 SSDT。
3.  创建一个设备，并将资源分配。 例如，对于如下所示的示例调用传感器设备**Platform.AddGenericDevice** ，并指定设备名称、 硬件 ID 和唯一的实例。 传感器设备连接到 I²C 串行总线 I2C1 DSDT 中所述。

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

下面是上述示例的输出。

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

## <a name="replacing-acpi-firmware-during-development-and-testing"></a>在开发和测试过程中替换 ACPI 固件

在开发和测试方案中，您可以替换的 AML 二进制文件从设备上 asl.exe 编译器生成的。 若要执行此操作，将 AML 二进制文件重命名为 acpitabl.dat 并将其移到 %windir%\\system32。 在启动时，Windows 使用 acpitabl.dat 中替换表中的 ACPI 固件存在。

**请注意**请确保启用测试签名。
**bcdedit /set testsigning 上**

## <a name="related-topics"></a>相关主题

[ACPI 系统说明表](acpi-system-description-tables.md)  
