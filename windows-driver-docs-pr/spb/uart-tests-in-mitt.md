---
title: MITT 中的 UART 测试
description: MITT 软件包包括用于验证到 UART 控制器及其驱动程序的数据传输的测试。 MITT 板的 UART 接口充当 UART 回送设备。
ms.assetid: 239F131C-5416-4E86-B0EE-E3156CDA11CF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a44070ec345f5785ddd210871f077abe3b964944
ms.sourcegitcommit: 0c3cab853b0b75149b7604eef03275f997792a84
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2020
ms.locfileid: "96157309"
---
# <a name="uart-tests-in-mitt"></a>MITT 中的 UART 测试

MITT 软件包包括用于验证到 UART 控制器及其驱动程序的数据传输的测试。 MITT 板的 UART 接口充当 UART 回送设备。

## <a name="before-you-begin"></a>开始之前

- 获取 MITT 板和 UART 适配器板。 请参阅 [购买使用 MITT 的硬件](./multi-interface-test-tool--mitt--.md)。
- [下载 MITT](/previous-versions/dn919810(v=vs.85))软件包。 在受测系统上安装它。
- 在 MITT 板上安装 MITT 固件。 请参阅 [MITT 入门](./get-started-with-mitt---.md)。

## <a name="hardware-setup"></a>硬件设置

![mitt uart 硬件设置](images/mitt-uart.jpg)

1. 需要外部引脚才能将 MITT 板上的 UART 接口连接到受测系统的 UART 控制器。 如果 UART 控制器公开了引脚，请直接连接到 **JB1** 板。
2. 连接这些行：

    | MITT 板上的 UART 接口 | 测试中的系统上的 UART 控制器 |
    |----------------------------------|------------------------------------------|
    | TX                               | RX                                       |
    | RTS                              | 限                                      |
    | RX                               | TX                                       |
    | 限                              | RTS                                      |

3. UART 适配器板提供了一个用于选择正确电压的跳线。 直接连接 (仅支持 3.3 V 信号，无需适配器板) 。

    ![uart 布线](images/uart-wiring.png)

## <a name="test-driver-and-acpi-configuration"></a>测试驱动程序和 ACPI 配置

若要修改 ACPI 表，请将 Windows 硬件认证包安装 (HCK) 8.1。 在具有 UART 控制器的受测系统上执行以下步骤：

1. 执行 BusController. HCKTestability 要求下所述的系统更改。
2. 根据 \\ \\ &lt; hckcontrollername &gt; \\ 测试 \\ &lt; 体系结构 &gt; UART Sample-UART 中提供 \\ 的模板更新 uart 测试驱动程序的 ACPI 表， \\ 或使用此示例。 你可以使用 [MICROSOFT ASL 编译器](../bringup/microsoft-asl-compiler.md)。

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

3. \\ \\ &lt; &gt; \\ \\ &lt; &gt; \\ 运行以下命令，通过 hckcontrollername 测试体系结构 UART 安装 UARTTest 测试外围设备：

    **pnputil – UARTTest**

## <a name="uart-automation-tests"></a>UART 自动化测试

1. 执行测试驱动程序和 ACPI 配置中所述的步骤。
2. 在要测试的系统上创建一个文件夹。
3. 将这些文件从% ProgramFiles (x86) % \\ Windows 工具包 \\ 8.1 \\ 测试 \\ 运行时 \\ TAEF 复制到该文件夹。
    - Wex.Common.dll
    - Wex.Communication.dll
    - Wex.Logger.dll

4. 从 MITT 软件包中复制 UtsSanity.exe 和 muttutil.dll。
5. 查看所有可用命令，启动 UtsSanity.exe-？ 并参阅可用的命令行选项：
    >[!NOTE]
    >在连接 MITT 板时运行测试需要 **– mitt** 选项。

示例1：在 115200 bps 运行测试 (默认值) 

`C:\\uart&gt; UtsSanity.exe –mitt`

示例2：在3Mbps 运行测试：

`C:\\uart&gt; UtsSanity.exe -mitt –baudRate 3000000`

## <a name="uart-adapter-schematic"></a>UART 适配器示意图

![spi 示意图](images/spi-schematic.png)
