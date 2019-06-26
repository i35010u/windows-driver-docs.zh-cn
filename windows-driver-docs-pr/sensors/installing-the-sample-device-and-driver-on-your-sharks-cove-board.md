---
title: Shark Cove 板上安装的示例设备和驱动程序
description: 请按照下列步骤安装示例驱动程序并将 ADXL345 加速感应器附加到 Shark Cove 板上的 J1C1 标头。
ms.assetid: A67EBD9C-9C5A-49D3-9205-37FC4396DF56
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be6def79b02e6ae72d48ef8908dbfdfb537d25b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377940"
---
# <a name="install-the-sample-device-and-driver-on-your-sharks-cove-board"></a>Shark Cove 板上安装的示例设备和驱动程序


请按照下列步骤安装示例驱动程序并将 ADXL345 加速感应器附加到 Shark Cove 板上的 J1C1 标头。

## <a name="install-windows-on-the-sharks-cove-board"></a>在 Sharks Cove 板上安装 Windows


有关如何获取 Shark Cove 看板以及如何在看板上安装 Windows 的信息，请参阅[Shark Cove 硬件开发板](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/sharks-cove-hardware-development-board)并[SharksCove.org](https://go.microsoft.com/fwlink/p/?linkid=403167)。

## <a name="modify-the-adxl345-to-work-with-the-sharks-cove"></a>修改用于 Shark Cove ADXL345


若要设置 ADXL345 I2C 模式中，连接到 CS 信号，输出 VDD 如下所示：

![adxl345 专题板](images/adxl-breakout-board.png)

## <a name="attach-the-modified-adxl345-to-the-sharks-cove"></a>将修改后的 ADXL345 附加到 Shark Cove


当 ADXL345 I2C 模式下运行时，将其附加到 Shark Cove 板上的 J1C1 标头。 如果电源连接器显示在左上角中，将看到在右下角中的此标头：

![j1c1 标头](images/j1c1-header.png)

将 ADXL345 pin 附加到 J1C1 标头插针，如下所示：

![j1c1 pin](images/pin-outs.png)

## <a name="install-kits-and-tools"></a>安装工具包和工具


一个驱动程序开发环境具有两台计算机：*主计算机*和*目标计算机*。 目标计算机也称为“测试计算机”  。 在主机上的 Microsoft Visual Studio 中开发和构建驱动程序。 调试程序在主机上运行并且位于 Visual Studio 用户界面中。 当测试和调试驱动程序时，驱动程序在目标计算机上运行。 在此情况下，Sharks Cove 板是目标计算机。

在主计算机上安装工具包和工具中所述[Shark Cove 硬件开发板](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/sharks-cove-hardware-development-board)。

## <a name="download-and-extract-the-spbaccelerometer-sample"></a>下载并提取 SpbAccelerometer 示例


在主计算机上转到[本页](https://go.microsoft.com/fwlink/p?linkid=506965)并单击下载按钮。 单击**保存**，然后单击**打开文件夹**。 右键单击 SpbAccelerometer 示例驱动程序 (UMDF 版本 1).zip，然后选择**全部提取**。 指定或浏览到为提取的文件的文件夹。 例如，无法提取到 c:\\SpbAccelerometer。

## <a name="open-the-driver-solution-in-visual-studio"></a>在 Visual Studio 中打开驱动程序解决方案


在主计算机上转到已提取的示例的文件夹。 双击解决方案文件，SpbAccelerometer.sln。 在 Visual Studio 中，找到解决方案资源管理器。 (如果尚未打开，请将此选择**解决方案资源管理器**从**视图**菜单。)在解决方案资源管理器，可以看到有两个项目的一种解决方案。 还有一个名为的驱动程序项目**SpbAccelerometer**和一个名为的包项目**包**（小写）。

## <a name="set-the-configuration-and-platform-in-visual-studio"></a>在 Visual Studio 中设置的配置和平台


在 Visual Studio 中，在解决方案资源管理器，右键单击**解决方案 SpbAccelerometer （2 个项目）** ，然后选择**Configuration Manager**。 设置配置和平台。 请确保配置**Win8.1 调试**，并将平台设置为**Win32**。 为驱动程序项目和包项目执行此操作。 不会检查**部署**框。

## <a name="build-the-sample-using-visual-studio"></a>使用 Visual Studio 生成示例


在 Visual Studio 中，在**构建**菜单中，选择**生成解决方案**。

## <a name="locate-the-built-driver-package"></a>找到生成的驱动程序包


在文件资源管理器，导航到包含内置的驱动程序包的文件夹。 例如，c:\\SpbAccelerometer\\Win8.1Debug\\包。

该包将包含这些文件：

| 文件                  | 描述                                                                       |
|-----------------------|-----------------------------------------------------------------------------------|
| SpbSamples.cat        | 签名的编录文件，可作为整个程序包的签名。      |
| SpbAccelerometer.inf  | 一个包含安装驱动程序所需信息的信息 (INF) 文件。 |
| WudfUpdate\_01011.dll | Wdf 共同安装程序。                                                          |
| SpbAccelerometer.dll  | 驱动程序文件中。                                                                  |



## <a name="alter-the-secondary-system-description-table-ssdt"></a>更改辅助系统描述表 (SSDT)


1.  将 x86 版本的 ASL.exe 复制到 Sharks Cove 板。 ASL.exe 包括 Windows Driver Kit (WDK) 中。

    例如：C:\\Program Files (x86)\\Windows Kits\\8.1\\Tools\\x86\\ACPIVerify\\ASL.exe

2.  Shark Cove 板上以管理员身份打开命令提示符窗口。 通过输入以下命令反编译 SSDT：

    **asl /tab=ssdt**

    这将创建 Ssdt.asl 文件。

3.  打开 Ssdt.asl（例如，在记事本中打开）。

    ``` syntax
    DefinitionBlock("SSDT.AML", "SSDT", 0x01, "Intel_", "ADebTabl", 0x00001000)
    {
        Scope()
        {
            Name(DPTR, 0x3bf2d000)
            Name(EPTR, 0x3bf3d000)
            Name(CPTR, 0x3bf2d010)
            Mutex(MMUT, 0x0)
            Method(MDBG, 0x1, Serialized)
            {
                Store(Acquire(MMUT, 0x3e8), Local0)
                If(LEqual(Local0, Zero))
                {
                    OperationRegion(ABLK, SystemMemory, CPTR, 0x10)
                    Field(ABLK, ByteAcc, NoLock, Preserve)
                    {
                        AAAA, 128
                    }
                    Store(Arg0, AAAA)
                    Add(CPTR, 0x10, CPTR)
                    If(LNot(LLess(CPTR, EPTR)))
                    {
                        Add(DPTR, 0x10, CPTR)
                    }
                    Release(MMUT)
                }
                Return(Local0)
            }
        }

        // Insert a Scope(_SB_) and a Device entry here.

    }
    ```

4.  插入 Scope(\_SB\_) 条目。 在 Scope 条目内，插入你自己的 Device 条目。 下面是一个作用域 (\_SB\_) 条目和 ADXL345 加速感应器设备条目。

    ``` syntax
    Scope(_SB_)
    {
        Device(SPBA)
        {
            Name(_HID, "SpbAccelerometer")
            Name(_UID, 1)



        Method(_CRS, 0x0, NotSerialized)
        {
            Name(RBUF, ResourceTemplate()
            {          
                I2CSerialBus(0x53, ControllerInitiated, 400000, AddressingMode7Bit, "\\_SB.I2C3", 0, ResourceConsumer) 
                GpioInt(Edge, ActiveHigh, Exclusive, PullDown, 0, "\\_SB.GPO2") {0x17}
            })

            Return(RBUF)
        }


        Method(_DSM, 0x4, NotSerialized)
        {
            If(LEqual(Arg0, Buffer(0x10)
            {
                0x1e, 0x54, 0x81, 0x76, 0x27, 0x88, 0x39, 0x42, 0x8d, 0x9d, 0x36, 0xbe, 0x7f, 0xe1, 0x25, 0x42
            }))
            {
                If(LEqual(Arg2, Zero))
                {
                    Return(Buffer(One)
                    {
                        0x03
                    })
                }

                If(LEqual(Arg2, One))
                {
                    Return(Buffer(0x4)
                    {
                        0x00, 0x01, 0x02, 0x03
                    })
                }
            }
            Else
            {
                Return(Buffer(One)
                {
                    0x00
                })
            }
        } // Method(_DSM ...)

    } // Device(SPBA)

} // Scope(_SB_)
```

在此示例中，`ResourceTemplate()` 下的条目指定加速计需要两个硬件资源：特定 I2C 总线控制器 (I2C3) 的连接 ID 和 GPIO 中断。 中断使用名为 GPO2 的 GPIO 控制器上的引脚 0x17。


5.  将自己的 Device 条目添加到 Ssdt.asl 之后，通过输入以下命令编译 Ssdt.asl：

    **asl ssdt.asl**

    这会将编译的输出放置在名为 Ssdt.aml 的文件中。

6.  验证是否已为 Sharks Cove 板启用测试签名。

    **注意**  测试签名将在预配期间自动启用。




在 Sharks Cove 板上，以管理员身份打开命令提示符窗口。 输入此命令：

**bcdedit /enum {current}**

验证是否可以在输出中看到 `testsigning Yes`。

``` syntax
Windows Boot Loader
-------------------
identifier              {current}
...
testsigning             Yes
...
```

如果需要手动启用测试签名，请参照以下步骤：

1.  以管理员身份打开命令提示符窗口，并输入此命令：

    **bcdedit /set TESTSIGNING ON**

2.  重启 Sharks Cove 板。 在开发板重启时，按住增大音量按钮。 转到  “设备管理器”&gt;“系统设置”&gt;“启动”。 将“UEFI 安全启动”  设置为“禁用”  。
3.  保存更改并继续启动到 Windows。


7.  若要加载已更新的 SSDT，请以管理员身份打开命令提示符窗口，并输入此命令：

    **asl /loadtable ssdt.aml**

    重启 Sharks Cove 板。

## <a name="install-and-run-the-sample-driver"></a>安装和运行示例驱动程序


1.  在主计算机上 Visual Studio 中打开 SpbAccelerometer 解决方案。
2.  在解决方案资源管理器，双击**包**（小写），然后选择**属性**。 转到**驱动程序安装 &gt; 部署**。 检查**启用部署**。 选中**部署前删除以前的驱动程序版本**。 有关**目标计算机名称**，输入以前预配你 Shark Cove 看板的名称。 选择**安装并验证**。 单击 **“确定”** 。
3.  上**调试**菜单中，选择**开始调试**。 驱动程序包会自动复制到 Shark Cove 板。 您的驱动程序将自动安装和加载。 Windows 用户模式下调试程序 （在 Visual Studio 中的主机计算机上运行） 会自动将附加到承载您的驱动程序的 Wudfhost.exe （Shark Cove 板上运行） 的实例。








