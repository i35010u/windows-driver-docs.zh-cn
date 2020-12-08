---
title: MITT 中的 I2C 控制器测试
description: MITT 软件包中包含的 i2c 测试模块可用于测试 i2c 控制器及其驱动程序的数据传输。 MITT 板充当连接到 I i2c 总线的客户端设备。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 332cc16c2da56a999215296d0015b9824ab07a5d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811849"
---
# <a name="i2c-controller-tests-in-mitt"></a>MITT 中的 I2C 控制器测试

MITT 软件包中包含的 i2c 测试模块可用于测试 i2c 控制器及其驱动程序的数据传输。 MITT 板充当连接到 I i2c 总线的客户端设备。

## <a name="before-you-begin"></a>在开始之前

- 获取 MITT 板和 i2c 适配器板。 请参阅 [购买使用 MITT 的硬件](./multi-interface-test-tool--mitt--.md)。
- [下载 MITT](/previous-versions/dn919810(v=vs.85))软件包。 在受测系统上安装它。
- 在 MITT 板上安装 MITT 固件。 请参阅 [MITT 入门](./get-started-with-mitt---.md)。

## <a name="hardware-setup"></a>硬件设置

![mitt i2c 硬件设置](images/i2csetup.png)

| 总线接口 | 固定                             | ACPI 和示意图 | 连接解决方案                |
|---------------|-------------------------------------|---------------------|------------------------------------|
| I i2c           |  (SCL、SDA 和 GND 所需的所有行)  | ACPI 表          | 调试板上 (简单的男块)  |

1. 将 i2c 适配器连接到 MITT 板上的 **JB1** 。

    ![mitt i2c 标头](images/i2cheader.png)

2. 使用 **JB1** 上的 i v C 标头 () ，在 3.3 v 与 1.8 v 之间选择正确的 i v c。 在此图中选择了 1.8 V。
3. 将适配器板上的 "SCL"、"SDA" 和 "GND" pin 连接到所测试系统上的已公开 SCL、SDA 和 GND 行。

    ![i2c 适配器](images/i2c-power.png)

4. 使用 I2C 适配器板上的跳线选择 3.3 V 与 1.8 V 之间的正确 I2C 电压。 在此图中，选择了 1.8 V。
5. 在 MITT 板上，将开关 **SW0** 设置为高位置。 当 MITT 处于开启状态时，此位置启用 I i2c 的默认模式。

    ![mitt 板上的 sw0](images/sw0.png)

6. 使用 " **重置** " 按钮重启 MITT 板。 如果到 I e 控制器的线路连接正确，请 **LD7** (SDA 指示器) 并 LD6 打开 **LD6** (SCL) 指示器。 如果任一 LED 未打开，则会出现线路问题，因为 SDA 或 SCL，或者两者都未被拉取。

## <a name="test-driver-and-acpi-configuration"></a>测试驱动程序和 ACPI 配置

在具有 I # C 控制器的受测系统上执行以下步骤：

1. 通过运行以下命令安装 MITT 软件包中包含的 WITTTest 驱动程序：

    **pnputil – witttest**

    ![mitt 板的安装 witt 驱动程序](images/mitt-install-witt.png)

>[!NOTE]
>PnpUtil.exe 包含在% SystemRoot% \\ System32 中。

2. 修改系统 ACPI，并包含此 ASL 表。 你可以使用 [MICROSOFT ASL 编译器](../bringup/microsoft-asl-compiler.md)。

  >[!NOTE]
>更改 " \\ \\ \_ SB \_ 。I2C2 "到要测试的 i2c 控制器的 ACPI 条目名称。

``` syntax
//TP1 100Khz Standard Target Device(TP1)
Device(TP1) {
    Name (_HID, "STK0001")
    Name (_CID, "WITTTest")
    Method(_CRS, 0x0, NotSerialized)
    {
      Name (RBUF, ResourceTemplate ()
      {
        I2CSerialBus ( 0x11, ControllerInitiated, 100000,AddressingMode7Bit, "\\_SB_.I2C2",,, , )
      })
      Return(RBUF)
    }
}

//TP2 400Khz  Fast Target
Device(TP2) {
    Name (_HID, "STK0002")
    Name (_CID, "WITTTest")
    Method(_CRS, 0x0, NotSerialized)
    {
      Name (RBUF, ResourceTemplate ()
      {
        I2CSerialBus ( 0x12, ControllerInitiated, 400000,AddressingMode7Bit, "\\_SB_.I2C2",,, , )
      })
      Return(RBUF)
    }
}

//TP3 1 Mhz  FastPlus Target
Device(TP3) {
    Name (_HID, "STK0003")
    Name (_CID, "WITTTest")
    Method(_CRS, 0x0, NotSerialized)
    {
      Name (RBUF, ResourceTemplate ()
      {
        I2CSerialBus ( 0x13, ControllerInitiated, 1000000,AddressingMode7Bit, "\\_SB_.I2C2",,, , )
      })
      Return(RBUF)
    }
  }
}

//TP4 1.4 Mhz High Speed, optional target
Device(TP4) {
    Name (_HID, "STK0004")
    Name (_CID, "WITTTest")
    Method(_CRS, 0x0, NotSerialized)
    {
      Name (RBUF, ResourceTemplate ()
      {
        I2CSerialBus ( 0x14, ControllerInitiated, 1400000,AddressingMode7Bit, "\\_SB_.I2C2",,, , )
      })
      Return(RBUF)
    }
}

//TP5 3.4 Mhz High Speed, optional target
Device(TP5) {
    Name (_HID, "STK0005")
    Name (_CID, "WITTTest")
    Method(_CRS, 0x0, NotSerialized)
    {
      Name (RBUF, ResourceTemplate ()
      {
        I2CSerialBus ( 0x15, ControllerInitiated, 3400000,AddressingMode7Bit, "\\_SB_.I2C2",,, , )
      })
      Return(RBUF)
    }
}
```

>[!NOTE]
>只需 TP1-3 即可运行 MITT I i2c 测试。 TP4 和 TP5 是可选目标。

## <a name="ic-automation-tests"></a>I i2c 自动测试

1. 在要测试的系统上创建一个文件夹。
2. 将 TAEF 二进制文件复制到该文件夹，然后将其添加到 PATH 环境变量中。 所需的 TAEF 二进制文件位于% ProgramFiles (x86) % \\ Windows 工具包 \\ 8.1 \\ 测试 \\ 运行时 \\ TAEF。
3. 将 Muttutil.dll 和 Mitti2ctest.dll 从 MITT 软件包复制到文件夹。
4. 使用 **/list** 选项查看所有 MITT I I C 测试：

    ![屏幕截图，在 "命令提示符" 中显示 MITT i 2 c 测试的列表。](images/mitt-i2c-cmds.png)

你现在已准备好运行 i2c 测试。 可以一次运行一个测试，也可以一次性运行测试，也可以手动运行测试。

- 使用 **/name： * &lt; test name &gt;*** 选项运行单个测试。 此命令运行 BasicIORead 测试：

  ![在 "命令提示符" 中显示单个测试运行的命令的屏幕截图。](images/mitt-i2c-cmds1.png)

- 使用此命令运行所有测试：

  ![mitt i2c 命令](images/mitt-i2c-cmds2.png)

- 使用 MITT 软件包中包含 SPBCmd.exe 工具手动运行测试。

## <a name="ic-adapter-schematic"></a>I i2c 适配器示意图

![i2c 示意图](images/i2c-schematic.png)
