---
title: MITT 中的 I2C 控制器测试
description: MITT 软件程序包中包含的 I²C 测试模块可用于测试 I²C 控制器和其驱动程序的数据传输。 MITT 板充当客户端设备连接到 I²C 总线。
ms.assetid: E40B9ABB-B119-4EC1-A383-EB96CC350A25
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c75ff728d0ec8fa36aac492c746e039fde3c61db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360240"
---
# <a name="i2c-controller-tests-in-mitt"></a>MITT 中的 I2C 控制器测试


**上次更新时间**

-   2015 年 1 月

**适用于：**

-   Windows 8.1

MITT 软件程序包中包含的 I²C 测试模块可用于测试 I²C 控制器和其驱动程序的数据传输。 MITT 板充当客户端设备连接到 I²C 总线。

## <a name="before-you-begin"></a>开始之前...


-   获取 MITT 板和 I²C 适配器板。 请参阅[购买硬件使用 MITT](https://msdn.microsoft.com/library/windows/hardware/dn919811)。
-   [下载 MITT 软件包](https://msdn.microsoft.com/library/windows/hardware/dn919810)。 待测试系统上安装它。
-   安装 MITT 固件 MITT 板上。 请参阅[开始使用 MITT](https://msdn.microsoft.com/library/windows/hardware/dn919779)。

## <a name="hardware-setup"></a>硬件安装


![mitt i2c 硬件安装](images/i2csetup.png)

| 总线接口 | 引出线                             | ACPI 和图表 | 连接解决方案                |
|---------------|-------------------------------------|---------------------|------------------------------------|
| I²C           | （SCL、 SDA 和 GND） 需要的所有行 | ACPI 表          | （在调试开发板） 的简单男性块 |



1.  连接到 I²C 适配器**JB1** MITT 板上。

    ![mitt i2c 标头](images/i2cheader.png)

2.  使用跳到 I²C 标头 (上面**JB1**) 来选择正确的 I²C 电压 3.3V 和 1.8 v 之间。 在此图中选定 1.8 v。
3.  适配器板上的 SCL、 SDA 和 GND 插针连接到待测试系统上公开的 SCL、 SDA 和 GND 行。

    ![i2c 适配器](images/i2c-power.png)

4.  用于跳线 I2C 适配器板上选择正确的 I2C 电压 3.3V 和 1.8 v 之间。 在此图中选定 1.8 v。
5.  MITT 板上将开关设置**SW0**到高的位置。 打开 MITT 时，此位置为 I²C 启用默认模式。

    ![sw0 mitt 板上](images/sw0.png)

6.  使用**重置**按钮到电源周期 MITT 板。 I²C 控制器的网络连接是正确的如果**LD7** （SDA 指标） 和**LD6** （SCL 指示器） 开启。 如果任一 led 指示灯没有亮起，因为 SDA 和 / 或，SCL，拉取低则接线问题。

## <a name="test-driver-and-acpi-configuration"></a>测试驱动程序和 ACPI 配置


具有 I²C 控制器的测试的系统上执行以下步骤：

1.  安装 WITTTest 驱动程序 MITT 软件程序包中包含通过运行以下命令：

    **pnputil –a witttest.inf**

    ![安装 witt mitt 板的驱动程序](images/mitt-install-witt.png)

    **请注意**PnpUtil.exe 包含在 %systemroot%\\System32。



2.  修改系统 ACPI，包括此 ASL 表。 可以使用[Microsoft ASL compiler](https://msdn.microsoft.com/library/windows/hardware/dn551195)。

    **请注意**更改"\\\\\_SB\_。I2C2"为 ACPI I²C 控制器，若要测试项名称。




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

**请注意**需要运行 MITT I²C 测试仅 TP1 3 个。 使用 TP4 和 TP5 是可选的目标。




## <a name="ic-automation-tests"></a>I²C 自动化测试


1.  待测试系统上创建一个文件夹。
2.  TAEF 二进制文件复制到的文件夹，然后将其添加到 PATH 环境变量。 必需的 TAEF 二进制文件位于 %programfiles （x86） %\\Windows 工具包\\8.1\\测试\\运行时\\TAEF。
3.  将 Muttutil.dll 和 Mitti2ctest.dll 从 MITT 软件程序包复制到的文件夹。
4.  通过查看所有 MITT I²C 测试 **/list**选项：

    ![mitt i2c 命令](images/mitt-i2c-cmds.png)

现在您就可以运行 I²C 测试。 可以运行单个测试，所有测试，或手动运行测试。

- 使用运行单个测试 **/name: *&lt;测试名称&gt;*** 选项。 此命令将运行 BasicIORead 测试：

  ![mitt i2c 命令](images/mitt-i2c-cmds1.png)

- 使用此命令运行所有测试：

  ![mitt i2c 命令](images/mitt-i2c-cmds2.png)

- 通过使用 MITT 软件程序包中包含的 SPBCmd.exe 工具手动运行测试。

## <a name="ic-adapter-schematic"></a>I²C 适配器示意图


![i2c 示意图](images/i2c-schematic.png)

## <a name="related-topics"></a>相关主题
[使用多接口测试工具 (MITT) 进行测试](https://msdn.microsoft.com/library/windows/hardware/dn919874)  



