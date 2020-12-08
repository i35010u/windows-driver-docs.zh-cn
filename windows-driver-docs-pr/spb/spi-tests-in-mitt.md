---
title: MITT 中的 SPI 测试
description: MITT 软件包中包含的 SPI 测试模块。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4138683a5e37b5c54bd0ca71d2cbc9e8f877ed84
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835401"
---
# <a name="spi-tests-in-mitt"></a>MITT 中的 SPI 测试

MITT 软件包中包含的 SPI 测试模块可用于测试数据传输是否适用于受测系统上的 SPI 控制器及其驱动程序。 MITT 板充当连接到 SPI 总线的客户端设备。

## <a name="before-you-begin"></a>在开始之前

- 获取 MITT 板、SPI 或 UART 适配器板。 请参阅 [购买使用 MITT 的硬件](./multi-interface-test-tool--mitt--.md)。
- [下载 MITT](/previous-versions/dn919810(v=vs.85))软件包。 在受测系统上安装它。
- 在 MITT 板上安装 MITT 固件。 请参阅 [MITT 入门](./get-started-with-mitt---.md)。

## <a name="hardware-setup"></a>硬件设置

![spi mitt 测试](images/spi.jpg)

| 总线接口 | 固定                                      | ACPI 和示意图 | 连接解决方案                  |
|---------------|----------------------------------------------|---------------------|--------------------------------------|
| SPI           | 需要 (SCLK、MISO、MOSI、SS、GND) 的所有行 | ACPI 表          | 调试板上的简单块标头 ()  |

1. 将 SPI 适配器连接到 MITT 板上的 **JC1** 。
2. 使用 SPI 适配器板上的跳线来选择正确的 SPI 电压。 跳线可用于在 3.3 V 与 1.8 V 之间进行选择。
3. 将 SCLK、MOSI、MISO、SS 和 GND 连接到受测系统。

    ![spi 布线](images/spiwiring.png)

4. 在 MITT 板上，将开关 **SW1** 设置为高位置。 当 MITT 处于开启状态时，此位置启用 SPI 的默认模式。 如果信号在 3.3 V 上，则可以直接将板 (连接到无 SPI 适配器板) 。

    ![spi 电源](images/spi-power.png)

## <a name="test-driver-and-acpi-configuration"></a>测试驱动程序和 ACPI 配置

在具有 I # C 控制器的受测系统上执行以下步骤：

1. 通过运行以下命令安装 MITT 软件包中包含的 WITTTest 驱动程序：

    **pnputil – witttest**

    ![mitt 板的安装 witt 驱动程序](images/mitt-install-witt.png)

    >[!NOTE]
    >PnpUtil.exe 包含在% SystemRoot% \\ System32 中。

2. 修改系统 ACPI，并包含此 ASL 表。 你可以使用 [MICROSOFT ASL 编译器](../bringup/microsoft-asl-compiler.md)。

    >[!NOTE]
    >更改 " \\ \\ \_ SB \_ 。SPI1 "到要测试的 SPI 控制器的 ACPI 条目名称，如下所示。 它定义了1Mhz、5Mhz 和20Mhz 上具有 SPI 频率的三个测试目标。

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

1. 在要测试的系统上创建一个文件夹。
2. 将 TAEF 二进制文件复制到该文件夹，然后将其添加到 PATH 环境变量中。 所需的 TAEF 二进制文件位于% ProgramFiles (x86) % \\ Windows 工具包 \\ 8.1 \\ 测试 \\ 运行时 \\ TAEF。
3. 将 Muttutil.dll 和 Mittspitest.dll 从 MITT 软件包复制到文件夹。
4. 使用 **/list** 选项查看所有 MITT SPI 测试：

现在，你可以运行 SPI 测试了。 可以一次运行一个测试，也可以一次性运行测试，也可以手动运行测试。

- 使用 **/name： * &lt; test name &gt;*** 选项运行单个测试。 此命令运行 BasicIORead 测试：
- 使用此命令运行所有测试：
- 使用 MITT 软件包中包含 SPBCmd.exe 工具手动运行测试。

## <a name="spi-adapter-schematic"></a>SPI 适配器示意图

![spi 示意图](images/spi-schematic.png)
