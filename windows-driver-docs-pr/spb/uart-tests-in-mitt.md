---
title: 在 MITT UART 测试
description: MITT 软件程序包包括用于验证数据传输到 UART 控制器和其驱动程序的测试。 MITT 板 UART 接口充当 UART 环回设备。
ms.assetid: 239F131C-5416-4E86-B0EE-E3156CDA11CF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee233cd76caccb9d34192b8ed56404ba6767f4b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521008"
---
# <a name="uart-tests-in-mitt"></a>在 MITT UART 测试


**上次更新时间**

-   2015 年 1 月

**适用于：**

-   Windows 8.1

MITT 软件程序包包括用于验证数据传输到 UART 控制器和其驱动程序的测试。 MITT 板 UART 接口充当 UART 环回设备。

## <a name="before-you-begin"></a>开始之前...


-   获取 MITT 板和 UART 适配器板。 请参阅[购买硬件使用 MITT](https://msdn.microsoft.com/library/windows/hardware/dn919811)。
-   [下载 MITT 软件包](https://msdn.microsoft.com/library/windows/hardware/dn919810)。 待测试系统上安装它。
-   安装 MITT 固件 MITT 板上。 请参阅[开始使用 MITT](https://msdn.microsoft.com/library/windows/hardware/dn919779)。

## <a name="hardware-setup"></a>硬件安装


![mitt uart 硬件安装](images/mitt-uart.jpg)

1.  需要外部引脚 MITT 板上的将 UART 接口连接到待测试系统 UART 控制器。 如果 UART 控制器公开引脚，直接连接到**JB1**的看板。
2.  连接这些行：

    | UART MITT 板上的接口 | 待测试系统上的 UART 控制器 |
    |----------------------------------|------------------------------------------|
    | TX                               | RX                                       |
    | RTS                              | CTS                                      |
    | RX                               | TX                                       |
    | CTS                              | RTS                                      |

     

3.  UART 适配器板提供用于选择正确的电压跳线。 仅 3.3V 信号支持直接连接 （而无需适配器开发板）。

    ![uart 布线](images/uart-wiring.png)

## <a name="test-driver-and-acpi-configuration"></a>测试驱动程序和 ACPI 配置


若要修改的 ACPI 表，请安装 Windows 硬件认证工具包 (HCK) 8.1。 具有 UART 控制器的测试的系统上执行以下步骤：

1.  执行 Device.BusController.UART.HCKTestability 要求下描述的系统更改。
2.  更新 UART 测试驱动程序基于下提供的模板的 ACPI 表\\ \\ &lt;hckcontrollername&gt;\\测试\\&lt;体系结构&gt;\\UART\\示例 UART.asl 或使用此示例。 可以使用[Microsoft ASL compiler](https://msdn.microsoft.com/library/windows/hardware/dn551195)。

    ``` syntax
    Device(UART) {
        Name (_HID, "UTK0001")
        Name (_CID, "UARTTest")
        Name (_UID,0)
        Method (_CRS, 0x0, NotSerialized) {
            Name (
                RBUF,
                ResourceTemplate () {
                    UARTSerialBus (
                        115200, // Baud Rate = 115200
                        DataBitsEight,
                        StopBitsOne,
                        0xC0,
                        LittleEndian,
                        ParityTypeNone,
                        FlowControlHardware, 
                        32,
                        32,
                        "\\_SB.UAR4",,,,
                    )
                }
            )
        Return(RBUF)
        }
    }
    ```

3.  安装 UARTTest 测试外围设备驱动程序从\\ \\ &lt;hckcontrollername&gt;\\测试\\&lt;体系结构&gt;\\通过 UART运行以下命令：

    **pnputil – a UARTTest.inf**

## <a name="uart-automation-tests"></a>UART 自动化测试


1.  执行测试驱动程序和 ACPI 配置中所述的步骤。
2.  待测试系统上创建一个文件夹。
3.  复制这些文件从 %programfiles （x86） %\\Windows 工具包\\8.1\\测试\\运行时\\TAEF 的文件夹。
    -   Wex.Common.dll
    -   Wex.Communication.dll
    -   Wex.Logger.dll

4.  将 UtsSanity.exe 和 muttutil.dll 复制从 MITT 软件程序包。
5.  查看可用的所有命令，启动 UtsSanity.exe-？ 和可用的命令行选项是指：**请注意**   **– mitt**选项是必需 MITT 板连接时在运行测试。

     

示例 1：若要在 115200 bps （默认值） 运行测试

**C:\\uart&gt; UtsSanity.exe – mitt**

示例 2：若要在 3 mbps 运行测试：

**C:\\uart&gt; UtsSanity.exe -mitt –baudRate 3000000**

## <a name="uart-adapter-schematic"></a>UART 适配器示意图


![spi 示意图](images/spi-schematic.png)

 

 




