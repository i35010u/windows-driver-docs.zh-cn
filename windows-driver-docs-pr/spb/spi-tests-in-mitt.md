---
title: MITT 中的 SPI 测试
description: SPI 测试 MITT 软件程序包中包含的模块。
ms.assetid: 8240841C-FFA0-48EC-AB7E-4E15E262C23D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8aa57f7d98267fede6aa847a28ed84410bb7ff8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376901"
---
# <a name="spi-tests-in-mitt"></a>MITT 中的 SPI 测试


**上次更新时间**

-   2015 年 1 月

**适用于：**

-   Windows 8.1

SPI MITT 软件程序包中包含的测试模块可用于测试 SPI 控制器测试和其驱动程序的系统上的数据传输。 MITT 板充当客户端设备连接到 SPI 总线。

## <a name="before-you-begin"></a>开始之前...


-   获取 MITT 板和 SPI 或 UART 适配器开发板。 请参阅[购买硬件使用 MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/multi-interface-test-tool--mitt--)。
-   [下载 MITT 软件包](https://docs.microsoft.com/previous-versions/dn919810(v=vs.85))。 待测试系统上安装它。
-   安装 MITT 固件 MITT 板上。 请参阅[开始使用 MITT](https://docs.microsoft.com/windows-hardware/drivers/spb/get-started-with-mitt---)。

## <a name="hardware-setup"></a>硬件安装


![spi mitt 测试](images/spi.jpg)

| 总线接口 | 引出线                                      | ACPI 和图表 | 连接解决方案                  |
|---------------|----------------------------------------------|---------------------|--------------------------------------|
| SPI           | （SCLK、 MISO、 MOSI、 SS、 GND） 需要的所有行 | ACPI 表          | 简单的块标头 （在调试开发板） |



1.  连接到的 SPI 适配器**JC1** MITT 板上。
2.  使用 SPI 适配器板上将跳线选择正确的 SPI 电压。 可以使用跳线 3.3V 和 1.8 v 之间进行选择。
3.  将 SCLK、 MOSI、 MISO、 SS 和 GND 连接到待测试系统。

    ![spi 布线](images/spiwiring.png)

4.  MITT 板上将开关设置**SW1**到高的位置。 打开 MITT 时，此位置为 SPI 启用默认模式。 如果信号的 3.3V，可直接连接 （不带 SPI 适配器开发板） 的看板。

    ![spi 电源](images/spi-power.png)

## <a name="test-driver-and-acpi-configuration"></a>测试驱动程序和 ACPI 配置


具有 I²C 控制器的测试的系统上执行以下步骤：

1.  安装 WITTTest 驱动程序 MITT 软件程序包中包含通过运行以下命令：

    **pnputil –a witttest.inf**

    ![安装 witt mitt 板的驱动程序](images/mitt-install-witt.png)

    **请注意**PnpUtil.exe 包含在 %systemroot%\\System32。



2.  修改系统 ACPI，包括此 ASL 表。 可以使用[Microsoft ASL compiler](https://docs.microsoft.com/windows-hardware/drivers/bringup/microsoft-asl-compiler)。

    **请注意**更改"\\\\\_SB\_。SPI1"到 ACPI SPI 控制器，以测试如下所示的条目名称。 它定义了三个测试目标，SPI 频率 1 Mhz、 5 Mhz 和 20 Mhz。




``` syntax
Device(TP1) {
    Name (_HID, "SPT0001") 
    Name (_CID, "WITTTest") 
    Method(_CRS, 0x0, NotSerialized)
    {
      Name (RBUF, ResourceTemplate ()
      {
          SpiSerialBus (0x0000, PolarityLow, FourWireMode, 0x08,ControllerInitiated, 0x000F4240, ClockPolarityLow,ClockPhaseFirst, "\\_SB.SPI1", 0x00, ResourceConsumer, , )
      })
      Return(RBUF)
    }
}
Device(TP2) {
    Name (_HID, "SPT0002") 
    Name (_CID, "WITTTest") 
    Method(_CRS, 0x0, NotSerialized)
    {
      Name (RBUF, ResourceTemplate ()
      {
          SpiSerialBus (0x0000, PolarityLow, FourWireMode, 0x08,ControllerInitiated, 0x004c4b40, ClockPolarityLow,ClockPhaseFirst, "\\_SB.SPI1", 0x00, ResourceConsumer, , )
      })
      Return(RBUF)
    }
}
Device(TP3) {
    Name (_HID, "SPT0003") 
    Name (_CID, "WITTTest") 
    Method(_CRS, 0x0, NotSerialized)
    {
      Name (RBUF, ResourceTemplate ()
      {
          SpiSerialBus (0x0000, PolarityLow, FourWireMode, 0x08,ControllerInitiated, 0x01312d00, ClockPolarityLow,ClockPhaseFirst, "\\_SB.SPI1", 0x00, ResourceConsumer, , )
      })
      Return(RBUF)
    }
}

```


## <a name="spi-automation-tests"></a>SPI 自动化测试


1.  待测试系统上创建一个文件夹。
2.  TAEF 二进制文件复制到的文件夹，然后将其添加到 PATH 环境变量。 必需的 TAEF 二进制文件位于 %programfiles （x86） %\\Windows 工具包\\8.1\\测试\\运行时\\TAEF。
3.  将 Muttutil.dll 和 Mittspitest.dll 从 MITT 软件程序包复制到的文件夹。
4.  通过查看所有 MITT SPI 测试 **/list**选项：

现在您就可以运行 SPI 测试。 可以运行单个测试，所有测试，或手动运行测试。

- 使用运行单个测试 **/name: *&lt;测试名称&gt;** * 选项。 此命令将运行 BasicIORead 测试：
- 使用此命令运行所有测试：
- 通过使用 MITT 软件程序包中包含的 SPBCmd.exe 工具手动运行测试。

## <a name="spi-adapter-schematic"></a>SPI 适配器示意图


![spi 示意图](images/spi-schematic.png)








